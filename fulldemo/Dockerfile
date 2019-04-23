FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["fulldemo/fulldemo.csproj", "fulldemo/"]
RUN dotnet restore "fulldemo/fulldemo.csproj"
COPY . .
WORKDIR "/src/fulldemo"
RUN dotnet build "fulldemo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "fulldemo.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "fulldemo.dll"]