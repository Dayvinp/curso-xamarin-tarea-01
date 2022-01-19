FROM mcr.microsoft.com/dotnet/aspnet:6.0-focal AS base
WORKDIR /app
EXPOSE 80

ENV ASPNETCORE_URLS=http://+:80

FROM mcr.microsoft.com/dotnet/sdk:6.0-focal AS build
WORKDIR /src
COPY ["src/MinimalWebAPI.csproj", "src/"]
RUN dotnet restore "src/MinimalWebAPI.csproj"
COPY . .
WORKDIR "/src/src"
RUN dotnet build "MinimalWebAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MinimalWebAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MinimalWebAPI.dll"]
