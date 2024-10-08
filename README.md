
Na versão prévia 6 do .NET 8, adicionamos novas APIs para permitir a exposição de endpoints para registrar, fazer login e atualizar tokens de portador. Esta é uma API simples
que retorna tokens (ou define cookies) que é otimizado para uso com aplicativos próprios (sem autenticação delegada). Os tokens são independentes e gerados usando o 
mesma técnica da autenticação por cookie. **Estes NÃO são JWTs**, são tokens independentes. Para fazer com que os tokens emitidos funcionem entre servidores, a [proteção de dados](https://learn.microsoft.com/en-us/aspnet/core/security/data-protection/configuration/overview?view=aspnetcore-7.0) precisa ser configurado
com armazenamento compartilhado.

## APIs

Existem 2 novos conceitos sendo introduzidos:

1. Um novo [manipulador de autenticação de token de portador](https://github.com/dotnet/aspnetcore/blob/bad855959a99257bc6f194dd19ecd6c9aeb03acb/src/Security/Authentication/BearerToken/src/BearerTokenExtensions.cs#L24). Este manipulador de autenticação suporta validação e emissão de token e integra
com o sistema de autenticação normal do ASP.NET Core. Pode ser usado de forma independente, sem identidade.
    - ASP.NET Core Identity se baseia nesse manipulador de autenticação e expõe um [AddIdentityBearerToken](https://github.com/dotnet/aspnetcore/blob/579d547d708eb19f8b05b00f5386649d6dac7b6a/src/Identity/Core/src/IdentityAuthenticationBuilderExtensions.cs# L20) .
2. [Um conjunto de endpoints HTTP](https://github.com/dotnet/aspnetcore/blob/bad855959a99257bc6f194dd19ecd6c9aeb03acb/src/Identity/Core/src/IdentityApiEndpointRouteBuilderExtensions.cs#L32) para registrar um novo usuário, trocar credenciais para um token/cookie e tokens de atualização usando as APIs de identidade.

Esses novos blocos de construção facilitam a criação de aplicativos próprios autenticados (aplicativos que não delegam autenticação).
