FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["TokenCore21/TokenCore21.csproj", "TokenCore21/"]
RUN dotnet restore "TokenCore21/TokenCore21.csproj"
COPY . .
WORKDIR "/src/TokenCore21"
RUN dotnet build "TokenCore21.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TokenCore21.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TokenCore21.dll"]