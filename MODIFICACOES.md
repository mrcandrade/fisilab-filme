# Modificações do Filme em relação ao FilmCraft

O Filme é o FilmCraft (https://github.com/storytold/filmcraft, versão 0.8.0) com a identidade
da **Suíte FisiLab**, disponibilizada pelo FisiLab — LARFIC · UFRGS em parceria com o CTA — Centro
de Tecnologia Acadêmica. Este arquivo lista o que foi alterado e por quê.

## O que mudou

### Nome e marca
- O nome visível passou de **FilmCraft** para **Filme**: título da janela, nome no
  `run_native`, menus (“About Filme”, “Quit/Hide Filme”, “Filme Help…”), diálogos,
  mensagens de erro e de status, notas das Preferências,
  instruções do servidor MCP, texto do `--help`/`--version` do aplicativo e da CLI e os catálogos
  de tradução (chaves e valores, em todos os idiomas).
- Onde “Filme” sozinho seria lido como o substantivo comum (o tipo de arquivo ou um recurso, e
  não o programa), o texto usa **FisiLab Filme**: filtro e tipo de arquivo de projeto (“FisiLab
  Filme Project”, “Selection as FisiLab Filme Project…”), modelos de gráficos (“FisiLab Filme
  Graphics Template”), mensagens “not a FisiLab Filme project/graphics template/keyboard shortcuts
  file”, nomes dos decodificadores (“FisiLab Filme H.264”…), nomes de renderizador mostrados,
  instruções e descrições do servidor MCP, relatório do sistema e o crédito do modelo de créditos.
- O NOTICE do FilmCraft diz que o nome, o logotipo e o wordmark do **ArtCraft** são marcas não
  cobertas pela licença livre. Por isso:
  - a pasta `docs/brand/` foi apagada e o módulo `crates/ui-egui/src/brand.rs` (que embutia o
    wordmark) foi removido; a janela Sobre e a tela Home não mostram mais o logotipo;
  - o botão “Discord” do cabeçalho virou o botão **Suíte FisiLab**, que abre a janela “Sobre a
    Suíte FisiLab”;
  - os links do menu Ajuda, da janela Sobre e da tela Home (Discord, site do ArtCraft, página do
    app em getartcraft.com, GitHub) foram trocados por: **Site da Suíte FisiLab**, **Manifesto
    pelas tecnologias livres**, **Projeto original (FilmCraft)** e **Reportar um problema**
    (issues de `mrcandrade/fisilab-filme`);
  - os créditos em texto ao ArtCraft Team e ao FilmCraft foram mantidos (são exigidos).
- Metadados de “programa criador” gravados em arquivos exportados (AAF, OMF, MXF, MCC, EBU STL,
  LUT `.cube`, `©too` do MP4, cabeçalho raster, campo `generator` do projeto) dizem “FisiLab Filme”.

### Identidade da Suíte FisiLab
- Novo crate compartilhado `crates/fisilab-brand` (paleta da marca, tela de abertura com a logo do CTA,
  janela “Sobre a Suíte FisiLab”), ligado ao aplicativo:
  - `APP_INFO` em `crates/ui-egui/src/lib.rs`;
  - `fisilab_brand::splash::enable()` em `apps/filmcraft/src/main.rs` (só no aplicativo desktop;
    `FISILAB_NO_SPLASH=1` desliga);
  - `fisilab_brand::frame(...)` a cada quadro em `FilmcraftApp::ui`;
  - item **Ajuda ▸ Sobre a Suíte FisiLab…** (`help.fisilab`), também no menu do app no macOS.
- Novo ícone (`assets/fisilab/fisilab-filme.ico` no executável Windows, `fisilab-filme-256.png` na janela).

### Paleta de cores
- Paleta original do FilmCraft, sem alterações de cor. Os temas originais ganharam os nomes **Noite**
  (escuro, o antigo Darkest, padrão) e **Dia** (claro, o antigo Light), primeiros da lista em Preferências ▸
  Aparência e em Exibir ▸ Aparência; o terceiro tema original (Dark) continua disponível. Os ids
  salvos (`darkest`, `dark`, `light`) não mudaram; `noite`/`night` e `dia`/`day` também são aceitos como nomes.
- O destaque padrão continua sendo o azul original.
- Português (Brasil) é o idioma da primeira execução (sem preferências salvas); a biblioteca continua com “idioma do sistema” como padrão.

### Idioma
- Numa instalação nova (sem `preferences.json`), a interface abre em **português do Brasil**. A
  escolha do usuário (outro idioma ou “Idioma do sistema”) é respeitada depois de salva. O padrão
  interno da preferência continua `system`, para que os testes e quem já tem preferências salvas
  não mudem.
- Textos novos da interface foram escritos em português, com traduções para espanhol, chinês e
  japonês (exigidas pelos testes de tradução).

### Executáveis, identificador e pastas
- Executáveis: `fisilab-filme(.exe)` e `fisilab-filme-cli(.exe)` (via `[[bin]]`; os nomes dos pacotes Cargo
  continuam `filmcraft` e `filmcraft-cli`). O alvo de log do executável é `fisilab_filme`, incluído
  no filtro padrão (`warn,filmcraft*=info,fisilab_filme=info`).
- Identificador do app: `br.ufrgs.fisilab.filme` (antes `ai.storyteller.filmcraft`); o arquivo
  `.desktop` do Linux foi renomeado para combinar.
- Pasta de dados: `%APPDATA%\FisiLab Filme` (macOS `~/Library/Application Support/FisiLab Filme`, Linux
  `~/.local/share/fisilab-filme`), para não misturar com uma instalação do FilmCraft. Pastas temporárias
  “FisiLab Filme Previews” e “FisiLab Filme Logs” (e “FisiLab Filme Previews” ao lado de um projeto salvo). O modo portátil (`portable.txt` + pasta `data`) não mudou.
- Recursos do executável Windows (`apps/filmcraft/build.rs`): ícone, ProductName, FileDescription,
  CompanyName, LegalCopyright, OriginalFilename e InternalName da Suíte FisiLab.
- O instalador MSI e o `package.ps1` (opcionais; a suíte usa um instalador Inno Setup próprio)
  usam os novos nomes, um novo UpgradeCode e links da suíte; o MSI instala em
  `Program Files\Suite FisiLab\Filme`, e o `portable.txt` do zip portátil aponta para
  `%APPDATA%\FisiLab Filme`.

### Outros
- A pasta `.github/` (CI, releases e financiamento do projeto original) foi apagada.
- O preset de atalhos padrão chama-se “FisiLab Filme Default”.
- Não há telemetria, verificação de atualizações nem envio de relatórios de falha no FilmCraft; os
  únicos downloads são os modelos opcionais de voz/transcrição do Hugging Face e do GitHub
  (mantidos).

## O que não mudou
- Todo o código de edição, codecs, formatos, efeitos e ferramentas.
- Nomes de crates, módulos, identificadores Rust, ids de comandos e de automação, variáveis de
  ambiente (`FILMCRAFT_*`), o servidor MCP (`filmcraft`) e o aplicativo web (que continua usando o
  mesmo código; só o título da página mudou).
- Formatos e extensões de arquivo (`.fcproj`, `.fcgt`…), as chaves usadas para ida e volta em
  AAF/OMF/OTIO, o `CreatorTool` dos XMP auxiliares e os nomes de renderizador gravados no projeto
  (a lista mostra “FisiLab Filme …”, mas o valor salvo é o original, por compatibilidade).
- LICENSE-MIT, LICENSE-APACHE, ATTRIBUTION.md e o texto original do NOTICE (agora após o
  cabeçalho da Suíte FisiLab). O README original está em `README.upstream.md`.
- Os empacotamentos de macOS, Linux e FreeBSD em `packaging/` não foram adaptados (fora do escopo
  da suíte, que distribui para Windows).
- A documentação em `docs/` (histórico do projeto original).
