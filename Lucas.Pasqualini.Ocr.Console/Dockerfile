FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Lucas.Pasqualini.Console/Lucas.Pasqualini.Console.csproj", "Lucas.Pasqualini.Console/"]
RUN dotnet restore "Lucas.Pasqualini.Console/Lucas.Pasqualini.Console.csproj"
COPY . .
WORKDIR "/src/Lucas.Pasqualini.Console"
RUN dotnet build "Lucas.Pasqualini.Console.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Lucas.Pasqualini.Console.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Lucas.Pasqualini.Console.dll"]
