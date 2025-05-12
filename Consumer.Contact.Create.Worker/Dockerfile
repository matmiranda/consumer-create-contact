FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Consumer.Contact.Create.Worker/Consumer.Contact.Create.Worker.csproj", "Consumer.Contact.Create.Worker/"]
COPY ["Consumer.Contact.Create.Domain/Consumer.Contact.Create.Domain.csproj", "Consumer.Contact.Create.Domain/"]
COPY ["Consumer.Contact.Create.Infrastructure/Consumer.Contact.Create.Infrastructure.csproj", "Consumer.Contact.Create.Infrastructure/"]
COPY ["Consumer.Contact.Create.Service/Consumer.Contact.Create.Service.csproj", "Consumer.Contact.Create.Service/"]
RUN dotnet restore "Consumer.Contact.Create.Api/Consumer.Contact.Create.Api.csproj"
COPY . .
WORKDIR "/src/Consumer.Contact.Create.Api"
RUN dotnet build -c Release -o /app/build
RUN dotnet publish -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENV ASPNETCORE_URLS=http://+:80
ENTRYPOINT ["dotnet", "Consumer.Contact.Create.Api.dll"]
