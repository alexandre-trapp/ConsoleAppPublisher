#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["App/ConsoleAppPublisher.csproj", "App/"]
RUN dotnet restore "App/ConsoleAppPublisher.csproj"
COPY . .
WORKDIR "/src/App"
RUN dotnet build "ConsoleAppPublisher.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ConsoleAppPublisher.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConsoleAppPublisher.dll"]