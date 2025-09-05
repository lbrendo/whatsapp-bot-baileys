# 🤖 WhatsApp Bot 24/7 (Grátis no Render) — Baileys

Este projeto sobe um bot de WhatsApp usando **Baileys** (sem Puppeteer) e um servidor **Express**.
Ele exibe uma página de **QR Code** (`/qr`), mantém a sessão salva no filesystem e, opcionalmente,
salva agendamentos no **Supabase**.

## ✅ Recursos
- Deploy em plano gratuito no Render (Web Service)
- Página `/qr` para escanear o QR sem precisar ver logs
- Endpoint `/send` para mandar mensagem de teste
- Integração opcional com Supabase (agenda)

## 📦 Variáveis de Ambiente (opcional para Supabase)
- `SUPABASE_URL`: URL do seu projeto
- `SUPABASE_KEY`: Chave (pode ser `service_role` se só o bot usar)
- `DEFAULT_USER_ID`: UUID do empresário (para vincular agenda)
- `SESSION_DIR`: (opcional) diretório de sessão, padrão `./sessions/default`

## 🚀 Como subir no Render
1. Suba este código em um repositório no GitHub.
2. No Render, crie um **Web Service** e conecte seu repositório.
3. Configure:
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
4. Adicione as variáveis de ambiente (se usar Supabase).
5. Abra a URL pública do serviço e visite `/qr` para escanear o código com o WhatsApp.
6. Após conectar, a página `/` mostrará `Status: connected`.

## 🧪 Teste de envio
Faça um POST para `/send`:
```bash
curl -X POST $RENDER_URL/send -H "Content-Type: application/json" -d '{"to":"5511999999999","message":"Olá do bot!"}'
```

## 🗂 Estrutura
```
server.js
package.json
```

## 🔒 Observações
- Não exponha chaves sensíveis do Supabase no frontend.
- O diretório `sessions/` será criado automaticamente e persistido no container enquanto o serviço estiver ativo. Em rebuilds frios o Render pode resetar o filesystem; se precisar persistência duradoura, considere armazenar o auth no Supabase Storage (não incluso aqui).
