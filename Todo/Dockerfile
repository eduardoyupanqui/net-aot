# 🐬 docker build -t eduyupanqui/todo-aot:1.0 .
# 🐬 docker run --rm -it -p 8080:8080 eduyupanqui/todo-aot:1.0
# ⚡ Usaremos la plataforma ligera de alpine linux: linux-musl-x64

# ✅ Usamos la imagen de SDK para compilar y publicar
FROM mcr.microsoft.com/dotnet/nightly/sdk:8.0-alpine-aot AS build
WORKDIR /source
# ✅ Copiamos el archivo de proyecto y restauramos las dependencias
COPY ./Todo.csproj .
RUN dotnet restore -r linux-musl-x64

# ✅ Copiamos el resto de los archivos y compilamos la aplicación
COPY . .
# ✅ Generamos los artefactos nativos que iran en el contenedor
RUN dotnet publish -c Release \
    -r linux-musl-x64 \
    -o /app Todo.csproj \
    --no-restore

# ✅ Usamos la imagen de runtime-deps para ejecutar la aplicación (7.55MB)
FROM mcr.microsoft.com/dotnet/nightly/runtime-deps:8.0-alpine-aot
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["/app/Todo"]