FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["SimpleApi/SimpleApi.csproj", "SimpleApi/"]
RUN dotnet restore "SimpleApi/SimpleApi.csproj"
COPY . .
WORKDIR "/src/SimpleApi"
RUN dotnet build "SimpleApi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SimpleApi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SimpleApi.dll"]