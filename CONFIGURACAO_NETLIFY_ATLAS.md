# Duda Tranças — Netlify + MongoDB Atlas

1. No MongoDB Atlas, crie um cluster (M0 gratuito, se disponível), um usuário de banco de dados com senha forte e obtenha a string de conexão em Connect > Drivers > Node.js. Substitua `<password>` pela senha codificada para URL, se necessário. Não exponha essa string no HTML nem no GitHub.
2. Em Network Access, autorize as conexões das Functions do Netlify. Como as Functions não têm IP de saída fixo no plano padrão, a configuração `0.0.0.0/0` pode ser necessária; **isso permite conexões de qualquer IP**. Use credenciais fortes e permissões mínimas, ou uma solução com IP fixo/restrição de rede para maior segurança.
3. No Netlify, no mesmo site já publicado, vá a Project configuration > Environment variables. Adicione:
   - `MONGODB_URI` = `mongodb+srv://USUARIO:SENHA@CLUSTER.mongodb.net/?retryWrites=true&w=majority`
   - `MONGODB_DB` = `duda_trancas` (opcional)
   - `ADMIN_PASSWORD` = sua senha forte de administração
   - `SESSION_SECRET` = segredo aleatório com pelo menos 32 caracteres
   Marque escopo Functions (ou All scopes).
4. Publique **este projeto inteiro**, incluindo `netlify/functions/api.js`, `package.json` e `netlify.toml`, preferencialmente via repositório Git conectado ao Netlify. O build deve instalar as dependências do package.json. Faça um novo deploy depois de salvar as variáveis.
5. Abra `/admin.html`, entre com a senha configurada, e teste um agendamento no site público em outro dispositivo. O site e o painel consultam `/api` periodicamente.

## Avisos importantes
- O Pix é **manual**: só marque como recebido após verificar o crédito no banco. Não há webhook de confirmação automática.
- O painel atual envia listas completas em atualizações administrativas; edições simultâneas de dois administradores podem gerar conflitos. Para produção com múltiplos administradores, recomenda-se migrar para endpoints de atualização por registro com controle de versão e transações.
- A sincronização é por consultas periódicas, não WebSocket; não é instantânea.
- O banco é criado automaticamente na primeira gravação. Nunca publique `MONGODB_URI` no código cliente.
