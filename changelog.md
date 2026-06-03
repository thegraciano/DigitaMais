Changelog — DigitaMais v2.3.0 — 2025-06-03🎨 Contraste & Legibilidade das Atividades

Revisão completa do contraste visual das letras na área de digitação, com foco em legibilidade para crianças
Letras pendentes saíram de tom quase invisível para texto escuro nítido sobre fundo roxo claro
Estado correto reforçado: verde mais escuro e saturado, peso de fonte aumentado para feedback imediato
Estado incorreto reforçado: vermelho mais profundo, diferenciação clara do estado neutro
Letra atual em destaque: borda e texto em azul-roxo escuro com contraste adequado para telas com brilho reduzido
Peso tipográfico das letras aumentado de 500 para 700
Bordas das teclas de atividade reforçadas de 1.5px para 2px
Modo sílabas recebeu o mesmo tratamento de contraste das letras individuais

⌨️ Teclado Virtual
Teclado virtual ampliado significativamente para melhor usabilidade em telas menores e para usuários mais jovens
Altura das teclas aumentada de 40px para 50px
Largura mínima das teclas aumentada de 28px para 38px
Tamanho da fonte aumentado de 11px para 14px com peso reforçado para 700
Teclas especiais e de pontuação também ampliadas proporcionalmente
Espaçamento entre teclas levemente aumentado
Cor do texto das teclas em repouso melhorada de cinza-roxo claro para #3b3366


Changelog — DigitaMais
v2.2.0 — 2025-06-02

🎨 Interface & Experiência Visual

Refatoração completa da identidade visual da plataforma com foco em aparência profissional, moderna e educacional

Layout reestruturado para melhor aproveitamento do espaço horizontal em desktop, reduzindo excesso de áreas vazias laterais

Container principal ampliado para criar sensação de plataforma premium em vez de mini aplicação centralizada

Área de digitação expandida e reposicionada para melhorar foco visual e leitura das palavras

Teclado virtual aproximado da atividade para criar fluxo visual contínuo entre leitura e digitação

Navbar reorganizada com hierarquia visual aprimorada:

informações importantes ganham destaque
elementos secundários foram suavizados
redução da aparência de “muitos botões soltos”

Tipografia refinada:

aumento de contraste das letras
melhoria no espaçamento entre caracteres
pesos tipográficos ajustados
legibilidade otimizada para crianças e adolescentes

Teclas da atividade redesenhadas:

bordas mais suaves
sombras sutis
melhor separação visual
aparência mais moderna e limpa

Profundidade visual adicionada:

sombras leves em containers e componentes
camadas suaves para evitar aparência totalmente flat
separação visual mais elegante entre áreas da interface

Paleta visual refinada:

branco mantido como cor predominante
roxo reduzido para função de destaque
saturação equilibrada
contraste geral melhorado

Teclado virtual redesenhado:

aparência mais próxima de teclado real
redução do visual “cartoon”
melhor feedback visual nas teclas
destaque da tecla ativa mais elegante

✨ Microinterações & Animações

Adicionadas microanimações suaves em:

hover de botões
troca de teclas
indicadores de status
transições entre fases

Tempo de animação padronizado para sensação de fluidez e responsividade

Redução de efeitos excessivos para experiência mais confortável e moderna

🧠 UX (Experiência do Usuário)

Fluxo visual reorganizado para manter atenção do usuário centralizada na digitação

Melhor distribuição de espaçamento vertical para evitar poluição visual

Interface otimizada para crianças do SCFV:

maior clareza visual
menos distrações
leitura mais confortável
aprendizado mais intuitivo

Melhoria na percepção de progressão e feedback visual durante atividades

🖼️ Fundo & Ambientação

Fundo pontilhado suavizado drasticamente para reduzir aparência genérica/template

Interface geral agora transmite:

sensação de plataforma educacional profissional
ambiente mais acolhedor
identidade visual mais sólida e memorável

🏷️ Branding

Nova identidade visual “DigitaMais” integrada à interface

Logo otimizada para:

reconhecimento infantil
aparência amigável
melhor escalabilidade
harmonia com a paleta visual do sistema

Consistência visual aplicada entre:

logo
botões
teclado
indicadores
telas de atividade

# Changelog — DigitaMais

## v2.1.0 — 2025-06-02

### 🔒 Segurança
- Senhas e nome de usuário admin migrados de texto puro para hashes SHA-256 via Web Crypto API nativa (sem dependências externas)
- Comparação de credenciais agora é 100% assíncrona e baseada em hash — nenhuma credencial fica legível no código-fonte
- `saveCredentials` passa a armazenar `userHash` e `passHash`; o valor original nunca é retido em memória após o hash
- Removido comentário instrucional que indicava como extrair senhas via console do navegador
- Adicionada função `esc()` de sanitização HTML (escapa `& < > " '`) aplicada a todos os pontos onde dados do usuário entram no DOM
- Corrigido XSS em `renderAdminWords`: palavras adicionadas pelo admin eram inseridas via `innerHTML` sem escape — reescrito com `createElement` + `textContent`
- Corrigido XSS na lista de resultados: `r.word` e nome do aluno entravam em `innerHTML` — substituído por construção segura via DOM
- Corrigido XSS no painel de celebração (`celeb-stats`): template string com `innerHTML` substituída por `createElement`
- Corrigido XSS no relatório PDF: `r.studentName`, `item.word`, `bestItem.word` e `worstItem.word` agora passam por `esc()` antes de entrar no template HTML
- Nome do aluno sanitizado e limitado a 60 caracteres na entrada

### 🎵 Áudio
- Trilha sonora de fundo substituída: BPM elevado de 72 para 130, onda `sine` trocada por `square` (estilo arcade), melodia reescrita em escala maior com contratempo e baixo marcado
- Adicionado som de contagem regressiva: beep curto nos números 3-2-1 e acorde ascendente no "VAI!"
- Adicionada fanfarra de vitória ao finalizar atividade (8 notas em progressão ascendente)

### 🐛 Correções
- Corrigido bug crítico em `finishGame`: referência a `#error-alert` (inexistente) trocada para `#high-error-alert` — impedia a tela de conclusão de aparecer ao terminar uma atividade
- Corrigido perda de foco ao alternar teclado virtual durante jogo: botão "Teclado" agora chama `focusInput()` após toggle, eliminando a necessidade de clicar no texto para continuar digitando

### ⌨️ Teclado Virtual
- Adicionado indicador de Caps Lock: badge âmbar animado aparece acima do teclado quando Caps Lock está ativo; tecla Caps Lock no teclado virtual é destacada em laranja
- Detecção de Caps Lock via `getModifierState` + listener no evento `keydown`
- Modo misto: teclas Shift (⇧) destacadas em verde com tooltip "Shift + [letra]" sempre que a próxima letra exigida for maiúscula, ensinando visualmente o uso correto do Shift no ABNT2
- Letras maiúsculas acentuadas também acionam o highlight do Shift junto à sequência de tecla morta
