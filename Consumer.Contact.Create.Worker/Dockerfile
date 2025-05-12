FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["Consumer.Contact.Create.Worker/Consumer.Contact.Create.Worker.csproj", "Consumer.Contact.Create.Worker/"]
COPY ["Consumer.Contact.Create.Application/Consumer.Contact.Create.Application.csproj", "Consumer.Contact.Create.Application/"]
COPY ["Consumer.Contact.Create.Domain/Consumer.Contact.Create.Domain.csproj", "Consumer.Contact.Create.Domain/"]
COPY ["Consumer.Contact.Create.Infrastructure/Consumer.Contact.Create.Infrastructure.csproj", "Consumer.Contact.Create.Infrastructure/"]
RUN dotnet restore "Consumer.Contact.Create.Worker/Consumer.Contact.Create.Worker.csproj"
COPY . .
WORKDIR "/src/Consumer.Contact.Create.Worker"
RUN dotnet build -c Release -o /app/build
RUN dotnet publish -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENV ASPNETCORE_URLS=http://+:80
ENTRYPOINT ["dotnet", "Consumer.Contact.Create.Worker.dll"]
