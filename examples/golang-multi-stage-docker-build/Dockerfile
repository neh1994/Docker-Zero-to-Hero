###########################################
# BASE IMAGE
###########################################

FROM ubuntu AS build

RUN apt-get update && apt-get install -y golang-go

ENV GO111MODULE=off

COPY . .

RUN CGO_ENABLED=0 go build -o /app .

############################################
# HERE STARTS THE MAGIC OF MULTI STAGE BUILD
############################################
##Empty Base Image: scratch is a special Docker image that is completely empty. It does not contain
#any operating system files, libraries, or utilities. This is often used for creating minimal images, 
#especially for statically compiled binaries, such as those built with Go.
##FROM scratch specifies that the image is starting from an empty base image.
#Using scratch results in a smaller final image because it includes only the compiled binary and nothing else,
#which minimizes the attack surface and reduces deployment times.
FROM scratch

# Copy the compiled binary from the build stage
COPY --from=build /app /app

# Set the entrypoint for the container to run the binary
ENTRYPOINT ["/app"]

