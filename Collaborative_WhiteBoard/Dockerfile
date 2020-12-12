#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Collaborative_WhiteBoard/Collaborative_WhiteBoard.csproj", "Collaborative_WhiteBoard/"]
RUN dotnet restore "Collaborative_WhiteBoard/Collaborative_WhiteBoard.csproj"
COPY . .
WORKDIR "/src/Collaborative_WhiteBoard"
RUN dotnet build "Collaborative_WhiteBoard.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Collaborative_WhiteBoard.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Collaborative_WhiteBoard.dll"]