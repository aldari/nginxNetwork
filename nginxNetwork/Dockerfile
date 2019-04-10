FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["nginxNetwork/nginxNetwork.csproj", "nginxNetwork/"]
RUN dotnet restore "nginxNetwork/nginxNetwork.csproj"
COPY . .
WORKDIR "/src/nginxNetwork"
RUN dotnet build "nginxNetwork.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "nginxNetwork.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENV ASPNETCORE_URLS=http://+:5000
EXPOSE 5000
ENTRYPOINT ["dotnet", "nginxNetwork.dll"]