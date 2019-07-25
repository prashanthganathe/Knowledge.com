FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["Knowledge.com/Knowledge.com.csproj", "Knowledge.com/"]
RUN dotnet restore "Knowledge.com/Knowledge.com.csproj"
COPY . .
WORKDIR "/src/Knowledge.com"
RUN dotnet build "Knowledge.com.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Knowledge.com.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Knowledge.com.dll"]