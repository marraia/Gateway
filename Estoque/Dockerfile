FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Estoque/Estoque.csproj Estoque/
RUN dotnet restore Estoque/Estoque.csproj
COPY . .
WORKDIR /src/Estoque
RUN dotnet build Estoque.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Estoque.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Estoque.dll"]
