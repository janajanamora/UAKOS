# ---------- 构建阶段 ----------
FROM mcr.microsoft.com/dotnet/sdk:9.0-preview AS build

# 1. 把整个仓库拷进来
WORKDIR /src
COPY . .

# 2. 进入 WebAPI 子目录   ←← 关键行
WORKDIR /src/UnsecuredAPIKeys.WebAPI

# 3. 还原依赖，Data 项目会被正确找到
RUN dotnet restore ./UnsecuredAPIKeys.WebAPI.csproj

# 4. 发布（包含 Data 依赖），输出到 /app
RUN dotnet publish ./UnsecuredAPIKeys.WebAPI.csproj -c Release -o /app

# ---------- 运行阶段 ----------
FROM mcr.microsoft.com/dotnet/aspnet:9.0-preview
WORKDIR /app
COPY --from=build /app .

ENV ASPNETCORE_URLS=http://0.0.0.0:${PORT}
EXPOSE 10000
ENTRYPOINT ["dotnet", "UnsecuredAPIKeys.WebAPI.dll"]
