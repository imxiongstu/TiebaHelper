#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["TiebaHelper.AspNetCore/TiebaHelper.AspNetCore.csproj", "TiebaHelper.AspNetCore/"]
RUN dotnet restore "TiebaHelper.AspNetCore/TiebaHelper.AspNetCore.csproj"
COPY . .
WORKDIR "/src/TiebaHelper.AspNetCore"
RUN dotnet build "TiebaHelper.AspNetCore.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TiebaHelper.AspNetCore.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TiebaHelper.AspNetCore.dll"]