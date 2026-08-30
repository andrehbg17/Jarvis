# J.A.R.V.I.S. — assistente pessoal

Um painel de comando estilo Homem de Ferro num **único arquivo**: `index.html`.
Não precisa instalar nada — é abrir no navegador de qualquer aparelho.

## O que ele faz agora

| Módulo | Como funciona | Precisa de internet? |
| --- | --- | --- |
| **Voz** | Fala com voz masculina em pt-BR e escuta pelo microfone (Chrome, Edge, Safari) | Não |
| **Chat com vários bots** | Grok (xAI), OpenAI, Groq ou Ollama local — você escolhe no painel "Cérebro" | Grok/OpenAI/Groq sim · **Ollama não** |
| **Clima mundial** | Qualquer cidade do planeta, com previsão (Open-Meteo, sem chave) | Sim |
| **Localização em tempo real** | GPS do próprio aparelho + endereço por extenso, atualizando enquanto você se move | GPS não, endereço sim |
| **Mercados** | Cotações ao vivo e gráfico de velas de BTC, ETH, SOL, BNB, XRP, DOGE, ADA + dólar/euro em reais | Sim |
| **Trading (simulação)** | Carteira virtual de US$ 10.000 com preços reais da Binance; compra/venda de treino, lucro/prejuízo salvo no aparelho | Sim |
| **Notícias ao vivo** | Manchetes do Google News em português (mundo, economia, tecnologia…) | Sim |
| **Tradutor** | Traduz entre 11 idiomas e fala a tradução em voz alta | Sim |

Comandos de voz/texto que já funcionam **sem configurar nada**:
`clima em Tóquio` · `onde estou` · `preço do bitcoin` · `cotação do dólar` ·
`notícias` · `traduzir bom dia para o inglês` · `que horas são` · `ajuda`

## Como abrir em cada aparelho

- **Notebook Windows (HP ou qualquer outro):** salve o `index.html` e dê dois
  cliques. Para o microfone funcionar, use Chrome ou Edge.
- **iPhone e Smart TV:** precisam de uma URL `https://` (regra do Safari e das
  TVs para microfone e GPS). Veja abaixo — leva uns 5 minutos e é grátis.

### Publicar numa URL grátis (para iPhone e TV)

O jeito mais fácil, sem saber programar — **Netlify Drop**:

1. No notebook, abra **https://app.netlify.com/drop**
2. Crie uma conta grátis (pode entrar com o e-mail) — sem conta o site expira
   em 24 horas; com conta é permanente.
3. Arraste a pasta `jarvis/` inteira (ou o arquivo `jarvis.zip`) para a página.
4. Em segundos aparece o endereço, algo como `https://seunome.netlify.app`.

Alternativa — **GitHub Pages**: crie um repositório **público** novo em
github.com (botão "New repository"), envie os arquivos da pasta `jarvis/` pelo
botão "uploading an existing file", e em **Settings → Pages** escolha
"Deploy from a branch" → `main`. A URL fica
`https://SEU-USUARIO.github.io/NOME-DO-REPO/`. (Este repositório aqui é
privado, e o plano gratuito do GitHub só publica Pages de repositório público —
por isso o repositório separado.)

### Instalar como app no iPhone

1. Abra a URL no **Safari** do iPhone.
2. Toque em **Compartilhar** (quadrado com seta) → **Adicionar à Tela de Início**.
3. O JARVIS vira um app com o ícone do reator arc, abre em tela cheia e,
   graças ao service worker, a interface abre até sem internet.
4. Na primeira vez, autorize microfone e localização quando o Safari pedir.

Na **Smart TV**, abra a mesma URL no navegador da TV — o layout aumenta
sozinho em telas grandes.

## Como conectar o Grok

1. Crie uma conta em **console.x.ai** e gere uma **API key** (é paga por uso,
   diferente da assinatura do X/Twitter).
2. No painel **Cérebro** do Jarvis, escolha "Grok (xAI)", cole a chave, modelo
   `grok-4`, e salve. A chave fica gravada **só no seu aparelho**.
3. Pronto: tudo que não for comando local vai para o Grok, e o Jarvis responde
   por escrito e por voz.

### Grok dentro do Obsidian

O Obsidian não tem Grok nativo, mas aceita por plugins de comunidade, porque a
API da xAI é compatível com o formato da OpenAI:

1. Obsidian → **Configurações → Plugins de comunidade** → desative o modo
   restrito → **Procurar**.
2. Instale **Copilot** (ou **Text Generator** — os dois servem).
3. Nas configurações do plugin, adicione um modelo personalizado
   (formato "OpenAI compatible" / "Custom"):
   - **Base URL:** `https://api.x.ai/v1`
   - **API key:** a mesma chave do console.x.ai
   - **Model:** `grok-4`
4. Agora o Grok conversa com as suas notas — esse é o "segundo cérebro":
   o plugin Copilot consegue indexar o cofre inteiro e responder com base no
   que você escreveu.

## Funcionar sem Wi-Fi

Dados ao vivo (clima, cotações, notícias) obviamente precisam de rede. O que
funciona offline: a interface toda, a voz, a carteira de treino salva — e o
**chat com IA**, se você instalar o [Ollama](https://ollama.com) no notebook:

```
ollama pull llama3.2
ollama serve
```

Depois escolha "Ollama local" no painel Cérebro. O modelo roda dentro do seu
HP, sem internet nenhuma.

## O que foi pedido e não dá para fazer (e por quê)

Sendo direto, porque promessa de filme não paga boleto:

- **"Saber de tudo" / "conectar em todos os sites da internet"** — nenhuma IA
  tem isso. O que existe é o que está aqui: APIs ao vivo para clima, mercado e
  notícias, mais um bot com busca (o Grok pesquisa a web quando conectado).
- **Trading com dinheiro real** — o painel entrega preços e gráficos reais,
  mas as ordens são simuladas de propósito. Ligar dinheiro de verdade exige
  chaves de corretora com permissão de saque/ordem dentro de uma página, o que
  é um risco enorme de segurança — e um bot autônomo operando sozinho é a
  forma mais rápida de perder dinheiro. Treine na simulação; se um dia quiser
  operar de verdade, isso se faz com a API oficial da corretora num servidor
  seu, nunca num HTML aberto na TV.
- **Rastrear "para onde vou" o tempo todo** — navegador só acessa GPS com a
  página aberta e com permissão sua. Rastreio contínuo em segundo plano é
  coisa de app nativo (e é bom que seja: ninguém quer uma página sabendo onde
  você está sem perguntar).
- **A voz exata do Jarvis do filme** — a voz é do ator Paul Bettany e é
  protegida. O Jarvis escolhe sozinho a melhor voz masculina do aparelho, e
  dá para melhorar muito:
  - **iPhone:** baixe a voz **Felipe** (Ajustes → Acessibilidade → Conteúdo
    Falado → Vozes → Português) — o Jarvis passa a usá-la sozinho.
  - **Windows:** abra o Jarvis no **Edge**, que expõe as vozes neurais
    "Antonio (Natural)" e "Daniel (Natural)".
  - **Voz de cinema:** crie uma conta grátis em **elevenlabs.io**, gere uma
    chave e cole no painel Cérebro — o Jarvis passa a falar com voz neural
    de altíssima qualidade (padrão: "Adam", grave; aceita outro voice ID).

### O microfone não responde?

1. **Permissão:** no Safari, toque no "aA"/cadeado na barra de endereço →
   Ajustes do Site → Microfone → Permitir.
2. **Ditado ligado:** Ajustes → Geral → Teclado → ative **Ditado** (o
   reconhecimento do Safari usa esse serviço).
3. **Fale logo após tocar no 🎙** — ele escuta por até 12 segundos.
4. **Alternativa infalível:** toque no campo de texto e use o microfone do
   teclado do iPhone; o Jarvis responde por voz do mesmo jeito.

## Privacidade

Chaves de API, histórico e carteira ficam no `localStorage` do navegador —
nada é enviado para servidor nenhum além das APIs públicas listadas no rodapé
da página.
