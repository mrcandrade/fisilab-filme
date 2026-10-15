# Janela do DMG (macOS)

Dois arquivos prontos, copiados por `package.sh` para dentro da imagem; nada é gerado durante o build.

| Arquivo | O que é |
|---|---|
| `background.tiff` | Fundo da janela do Finder (HiDPI, 1x e 2x). Vai para `.background/background.tiff`. |
| `dmg-layout.DS_Store` | Ajustes de visualização do volume (tamanho da janela, ícones, posições e fundo). Vai para `.DS_Store`. |

Os dois vêm de `suite-fisilab/scripts/gerar_mac.py`, no repositório
[mrcandrade/larfic](https://github.com/mrcandrade/larfic). Não edite à mão: gere de novo por lá.

O layout espera:

- volume chamado exatamente `Filme` (sem versão: o Finder acha o fundo pelo nome do volume);
- o aplicativo em `Filme.app`;
- o atalho para `/Applications` chamado `Aplicativos`.
