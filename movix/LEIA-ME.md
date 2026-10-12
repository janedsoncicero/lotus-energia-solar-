# MoviX: landing page

Página: `movix/index.html`. É um arquivo único, sem dependências, e pode ser hospedado em qualquer lugar (GitHub Pages, Netlify, Vercel, Hostinger, etc.).

## Arquivos

| Arquivo | Para que serve |
| --- | --- |
| `index.html` | A landing page com o funil de cadastro |
| `google-apps-script.gs` | Script que salva os cadastros em uma planilha Google |
| `logo-movix-wordmark.png` | Logo do topo (fundo transparente) |
| `logo-movix-full.png` | Logo com slogan, usada no rodapé |
| `logo-movix-original.jpg` | Arte original da logo (também usada na prévia de links) |
| `favicon.png` | Ícone da aba do navegador |

## O funil

1. **Você já trabalha com rastreamento?**
   - **Sim** → quantas placas (até 50 / 51–100 / 101–150 / mais de 150) → plataforma atual (opcional) → dificuldades → o que ajudaria → contato
   - **Não** → já tem clientes interessados? → (se sim) quantas placas → quando quer começar (imediatamente / 1 mês / 3 meses / pesquisando) → quanto quer investir (R$ 300 a R$ 10.000+) → contato
2. **Contato:** nome, WhatsApp, cidade/UF, e-mail (opcional) e autorização de contato.

Todo cadastro vai para a planilha com: respostas do funil, contato, link direto para abrir a conversa no WhatsApp, coluna **Status** (Novo, Em contato, Proposta enviada, Fechado, Perdido) e a origem do anúncio (`utm_source`, `utm_campaign`, `utm_content`...).

Depois de enviar, a pessoa vê um botão para chamar a MoviX no WhatsApp com uma mensagem já preenchida com o resumo do cadastro.

## Configuração (uma vez só, cerca de 5 minutos)

### 1. Criar a planilha e o script
1. Crie uma planilha nova no Google Sheets (ex.: "MoviX - Leads").
2. Menu **Extensões → Apps Script**.
3. Apague o conteúdo do editor, cole todo o conteúdo de `google-apps-script.gs` e salve.
4. Clique em **Implantar → Nova implantação**.
   - Tipo: **App da Web**
   - Executar como: **Eu**
   - Quem pode acessar: **Qualquer pessoa**
5. Autorize o acesso quando o Google pedir e copie a **URL do app da Web** (termina em `/exec`).

### 2. Ligar a página à planilha
No `index.html`, procure por `CONFIG` (perto do início do `<script>`) e preencha:

```js
const CONFIG = {
  SCRIPT_URL: "https://script.google.com/macros/s/XXXXXXXX/exec",
  WHATSAPP: "5511999998888"   // número da MoviX: 55 + DDD + número, só números
};
```

### 3. Testar
Abra a página, faça um cadastro de teste e confira se a linha apareceu na aba **Leads** da planilha.

> Se você alterar o script depois, use **Implantar → Gerenciar implantações → Editar → Nova versão** para a URL continuar a mesma.

## Cores e textos
- As cores ficam no topo do `<style>`, em `:root` (`--accent`, `--accent-2`, `--grad`).
- Perguntas e opções do funil ficam no objeto `STEPS` dentro do `<script>`.

## Pixel / Google Tag Manager
Se o Pixel da Meta (`fbq`) ou o GTM (`dataLayer`) estiverem instalados na página, um cadastro concluído dispara automaticamente o evento `Lead` / `lead_movix`.
