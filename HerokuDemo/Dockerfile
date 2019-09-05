FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["HerokuDemo.csproj", "HerokuDemo/"]
RUN dotnet restore "HerokuDemo/HerokuDemo.csproj"
COPY . "./HerokuDemo"
WORKDIR "/src/HerokuDemo"
RUN dotnet build "HerokuDemo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HerokuDemo.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
CMD dotnet HerokuDemo.dll