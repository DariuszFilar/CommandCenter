FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

COPY ["CommandCenter/CommandCenter.csproj", "CommandCenter/"]
RUN dotnet restore "CommandCenter/CommandCenter.csproj"

COPY . .
WORKDIR /src/CommandCenter
RUN dotnet publish -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

ENV ASPNETCORE_URLS=http://0.0.0.0:${PORT}
EXPOSE 8080

COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "CommandCenter.dll"]