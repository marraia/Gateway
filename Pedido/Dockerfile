FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Pedido/Pedido.csproj Pedido/
RUN dotnet restore Pedido/Pedido.csproj
COPY . .
WORKDIR /src/Pedido
RUN dotnet build Pedido.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Pedido.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Pedido.dll"]
