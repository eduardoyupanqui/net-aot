# 🐬 docker build -t eduyupanqui/todo-aot:1.0 .
# 🐬 docker run --rm -it -p 8080:8080 eduyupanqui/todo-aot:1.0
# ⚡We use runtime alpine: linux-musl-x64

FROM mcr.microsoft.com/dotnet/nightly/sdk:8.0-alpine-aot AS build
WORKDIR /source
COPY ./Todo.csproj .
RUN dotnet restore \
    -r linux-musl-x64
COPY . .
RUN dotnet publish \
    -c Release \
    -r linux-musl-x64 \
    -o /app Todo.csproj \
    --no-restore

FROM mcr.microsoft.com/dotnet/nightly/runtime-deps:8.0-alpine-aot
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["/app/Todo"]