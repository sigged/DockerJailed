FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 51743
EXPOSE 44344

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["/DockerJailed/DockerJailed.csproj", "DockerJailed/"]
RUN dotnet restore "DockerJailed/DockerJailed.csproj"
COPY . .
WORKDIR "/src/DockerJailed"
RUN dotnet build "DockerJailed.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DockerJailed.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerJailed.dll"]