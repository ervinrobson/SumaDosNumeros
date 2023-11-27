# Usa la imagen de ASP.NET Core como base
FROM mcr.microsoft.com/dotnet/core/aspnet:latest AS base
WORKDIR /app
EXPOSE 80

# Usa la imagen de SDK de .NET Core para compilar el código
FROM mcr.microsoft.com/dotnet/core/sdk:latest AS build
WORKDIR /src
COPY ["SumaDosNumeros.csproj", "."]
RUN dotnet restore "./SumaDosNumeros.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "SumaDosNumeros.csproj" -c Release -o /app/build

# Publica la aplicación
FROM build AS publish
RUN dotnet publish "SumaDosNumeros.csproj" -c Release -o /app/publish

# Configura la imagen final
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SumaDosNumeros.dll"]
