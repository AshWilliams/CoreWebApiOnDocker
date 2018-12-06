FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["WebApiTestCont/WebApiTestCont.csproj", "WebApiTestCont/"]
RUN dotnet restore "WebApiTestCont/WebApiTestCont.csproj"
COPY . .
WORKDIR "/src/WebApiTestCont"
RUN dotnet build "WebApiTestCont.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApiTestCont.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApiTestCont.dll"]