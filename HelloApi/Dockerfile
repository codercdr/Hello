FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["HelloApi/HelloApi.csproj", "HelloApi/"]
RUN dotnet restore "HelloApi/HelloApi.csproj"
COPY . .
WORKDIR "/src/HelloApi"
RUN dotnet build "HelloApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HelloApi.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=publish /app/publish .
EXPOSE 5000
EXPOSE 5001
ENV ASPNETCORE_URLS=http://+:5000;https://+:5001
ENTRYPOINT ["dotnet", "HelloApi.dll"]