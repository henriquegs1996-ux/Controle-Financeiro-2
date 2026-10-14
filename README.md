# Controle Financeiro Web

Aplicação de controle financeiro pessoal feita em HTML, CSS e JavaScript, pronta para publicar no GitHub Pages.

## Publicar no GitHub Pages

1. Crie um repositório no GitHub, por exemplo `controle-financeiro`.
2. Envie o arquivo `index.html` para a raiz do repositório.
3. Abra **Settings → Pages**.
4. Em **Build and deployment**, selecione **Deploy from a branch**.
5. Escolha a branch `main` e a pasta `/ (root)`, depois clique em **Save**.
6. Aguarde a publicação. O endereço será semelhante a `https://SEU-USUARIO.github.io/controle-financeiro/`.

## Recursos

- Página inicial e dashboard com indicadores e gráficos.
- Planos de contas editáveis para receitas, despesas e investimentos.
- Cadastro, edição, exclusão e consulta de lançamentos.
- Filtros por período, mês, ano, tipo, categoria e texto.
- Relatórios anuais, gráficos e sugestões automáticas de melhoria.
- Exportação de lançamentos em CSV e backup em JSON.

## Atenção aos dados

Os registros ficam no `localStorage` do navegador e não são sincronizados entre dispositivos nem compartilhados entre navegadores. Limpar os dados do navegador pode apagá-los. Use **Exportar backup** regularmente. Para vários usuários, sincronização entre dispositivos ou acesso seguro por login, será necessário conectar um backend/banco de dados.

Não publique dados financeiros pessoais reais em arquivos do repositório. O `index.html` não contém seus lançamentos; eles ficam no navegador.


## Responsividade

A interface adapta menus, cartões, filtros e gráficos para computadores, tablets e celulares. Em telas pequenas, o menu fica horizontal e as tabelas podem ser roladas lateralmente.

## Sincronização na nuvem entre dispositivos (Supabase)

A sincronização requer configurar um projeto Supabase. Sem essa configuração, o aplicativo continua funcionando localmente no navegador.

1. Crie um projeto em https://supabase.com/ e copie a Project URL e a publishable/anon key em Project Settings → API. A chave pública pode ficar no frontend; nunca use `service_role`.
2. No SQL Editor do Supabase, execute:

```sql
create table if not exists public.finance_data (
  user_id uuid primary key references auth.users(id) on delete cascade,
  payload jsonb not null default '{}'::jsonb,
  updated_at timestamptz not null default now()
);
alter table public.finance_data enable row level security;
create policy "Users can read their own finance data"
  on public.finance_data for select to authenticated using (auth.uid() = user_id);
create policy "Users can insert their own finance data"
  on public.finance_data for insert to authenticated with check (auth.uid() = user_id);
create policy "Users can update their own finance data"
  on public.finance_data for update to authenticated using (auth.uid() = user_id) with check (auth.uid() = user_id);
```

3. Publique o site no GitHub Pages. Em cada dispositivo, abra **Sincronização**, informe a mesma Project URL, a mesma chave pública e entre com o mesmo e-mail/senha. Se a confirmação de e-mail estiver ativada, confirme o e-mail antes de entrar.
4. O app salva localmente e envia alterações para a nuvem quando há sessão autenticada. Ao conectar em um dispositivo novo, ele carrega os dados existentes da nuvem.

**Atenção:** a primeira conexão de um usuário sem registro na nuvem envia os dados locais para a nuvem. Ao conectar um dispositivo que já tenha dados locais diferentes dos dados da nuvem, faça backup antes; a cópia existente na nuvem será carregada no dispositivo.
