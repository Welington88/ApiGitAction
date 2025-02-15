#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["ApiGitAction.csproj", "."]
RUN dotnet restore "./ApiGitAction.csproj"
COPY . .
RUN pwd
RUN ls -l
WORKDIR "/src/."
RUN dotnet build "ApiGitAction.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ApiGitAction.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ApiGitAction.dll"]
