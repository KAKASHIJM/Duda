# Duda Tranças — sincronização real

1. Crie um site no Netlify e envie este projeto por GitHub (recomendado). Netlify instala dependências do package.json.
2. Em Site configuration > Environment variables, configure:
   - `DATABASE_URL`: string de conexão PostgreSQL do Neon (com SSL).
   - `ADMIN_PASSWORD`: sua senha privada do painel (ex.: a senha já escolhida, sem colocar no HTML).
   - `SESSION_SECRET`: sequência aleatória forte de pelo menos 32 caracteres.
3. Faça novo deploy. Abra `/` para clientes e `/admin.html` para administração.
4. O banco cria as tabelas automaticamente na primeira requisição. Teste uma reserva e confira no painel em outro aparelho.
5. As reservas ficam com Pix manual: somente marque como recebido após verificar o extrato bancário. Não há confirmação automática de pagamento.

ATENÇÃO: conexão Neon e senha não devem ser colocadas no HTML nem enviadas ao GitHub. A API valida senha no servidor. Atualização a cada 8–10 segundos, não WebSocket. O painel usa substituição de conjuntos de dados; evite dois administradores editando ao mesmo tempo. Para produção com grande volume, migre as operações para alterações individuais transacionais.
