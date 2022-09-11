#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["Azure7Handson/Azure7Handson.csproj", "Azure7Handson/"]
RUN dotnet restore "Azure7Handson/Azure7Handson.csproj"
COPY . .
WORKDIR "/src/Azure7Handson"
RUN dotnet build "Azure7Handson.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Azure7Handson.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Azure7Handson.dll"]