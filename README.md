## APIs

Na versão prévia 6 do .NET 8, adicionamos novas APIs para permitir a exposição de endpoints para registrar, fazer login e atualizar tokens de portador. Esta é uma API simples
que retorna tokens (ou define cookies) que é otimizado para uso com aplicativos próprios (sem autenticação delegada). Os tokens são independentes e gerados usando o 
mesma técnica da autenticação por cookie. **Estes NÃO são JWTs**, são tokens independentes. Para fazer com que os tokens emitidos funcionem entre servidores, a [proteção de dados](https://learn.microsoft.com/en-us/aspnet/core/security/data-protection/configuration/overview?view=aspnetcore-7.0) precisa ser configurado
com armazenamento compartilhado.

Esses novos blocos de construção facilitam a criação de aplicativos próprios autenticados (aplicativos que não delegam autenticação).
