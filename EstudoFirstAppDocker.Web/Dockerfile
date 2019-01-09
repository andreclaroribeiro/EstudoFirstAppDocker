FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["EstudoFirstAppDocker.Web/EstudoFirstAppDocker.Web.csproj", "EstudoFirstAppDocker.Web/"]
RUN dotnet restore "EstudoFirstAppDocker.Web/EstudoFirstAppDocker.Web.csproj"
COPY . .
WORKDIR "/src/EstudoFirstAppDocker.Web"
RUN dotnet build "EstudoFirstAppDocker.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "EstudoFirstAppDocker.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "EstudoFirstAppDocker.Web.dll"]