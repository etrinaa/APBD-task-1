FROM mcr.microsoft.com/dotnet/runtime:8.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Tutorial1/Tutorial1.csproj", "Tutorial1/"]
RUN dotnet restore "Tutorial1/Tutorial1.csproj"
COPY . .
WORKDIR "/src/Tutorial1"
RUN dotnet build "Tutorial1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Tutorial1.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Tutorial1.dll"]
