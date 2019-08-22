FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["DockerHelloWorld/DockerHelloWorld.csproj", "DockerHelloWorld/"]
RUN dotnet restore "DockerHelloWorld/DockerHelloWorld.csproj"
COPY . .
WORKDIR "/src/DockerHelloWorld"
RUN dotnet build "DockerHelloWorld.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DockerHelloWorld.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerHelloWorld.dll"]