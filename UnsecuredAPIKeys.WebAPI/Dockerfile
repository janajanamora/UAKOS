# ---------- 用 SDK 镜像编译 ----------
FROM mcr.microsoft.com/dotnet/sdk:9.0-preview AS build
WORKDIR /src
COPY . .

# ① 进入子目录再还原依赖
WORKDIR /src/UnsecuredAPIKeys.WebAPI
RUN dotnet restore

# ② 继续在同一目录发布
RUN dotnet publish -c Release -o /app

# ---------- 用运行时镜像启动 ----------
FROM mcr.microsoft.com/dotnet/aspnet:9.0-preview
WORKDIR /app
COPY --from=build /app .

ENV ASPNETCORE_URLS=http://0.0.0.0:${PORT}
EXPOSE 10000
ENTRYPOINT ["dotnet", "UnsecuredAPIKeys.WebAPI.dll"]
