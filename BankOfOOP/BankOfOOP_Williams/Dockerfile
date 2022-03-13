#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:3.1 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["BankOfOOP_Williams/BankOfOOP_Williams.csproj", "BankOfOOP_Williams/"]
RUN dotnet restore "BankOfOOP_Williams/BankOfOOP_Williams.csproj"
COPY . .
WORKDIR "/src/BankOfOOP_Williams"
RUN dotnet build "BankOfOOP_Williams.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BankOfOOP_Williams.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BankOfOOP_Williams.dll"]