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
- Relatórios mensais ou anuais filtráveis, com opção de imprimir/salvar em PDF e sugestões automáticas de melhoria.
- Temas prontos e personalização de cores principal, destaque e fundo.
- Exportação de lançamentos em CSV e backup em JSON.

## Exportar PDF

Na seção **Relatórios**, escolha Mensal ou Anual, selecione mês/ano e clique em **Baixar relatório em PDF**. Na janela de impressão do navegador, escolha **Salvar como PDF**.

## Atenção aos dados

Os registros ficam no `localStorage` do navegador e não são sincronizados entre dispositivos nem compartilhados entre navegadores. Limpar os dados do navegador pode apagá-los. Use **Exportar backup** regularmente. Para vários usuários, sincronização entre dispositivos ou acesso seguro por login, será necessário conectar um backend/banco de dados.

Não publique dados financeiros pessoais reais em arquivos do repositório. O `index.html` não contém seus lançamentos; eles ficam no navegador.
