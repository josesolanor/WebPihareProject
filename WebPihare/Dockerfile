FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["WebPihare/WebPihare.csproj", "WebPihare/"]
RUN dotnet restore "WebPihare/WebPihare.csproj"
COPY . .
WORKDIR "/src/WebPihare"
RUN dotnet build "WebPihare.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebPihare.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebPihare.dll"]