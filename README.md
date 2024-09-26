**Issue:**
The Dockerfile grows large because it installs several tools, libraries, and dependencies without any optimization. This will cause issues when running on public agents with size limitations.

**Optimizing the Multistage Dockerfile**
We can optimize this Dockerfile in the following ways:

- Remove unnecessary intermediate files after each installation.
- Combine layers to minimize size.
- Use smaller base images like alpine where possible (for tools that don't need full Ubuntu-based images).
- Use multi-stage builds to reduce the final image size.

# DockerFile-Optimization
Optimized Azure Build Agent Docker Image with Multiple CLIs
Overview
This repository contains a Dockerfile that builds a custom Azure Build Agent image optimized for size, containing various CLIs and tools commonly used in development pipelines, such as:

Azure CLI
Node.js (npm)
Java (OpenJDK 11)
Terraform
Cucumber
Shell/Bash
The initial image grew too large for use on public agents due to its size. This repository includes an optimized multi-stage Docker build that reduces the image size by combining layers and removing unnecessary files after installations.

CLIs Included
Azure CLI (via base image)
Node.js & npm
Java 11 (OpenJDK)
Terraform
Cucumber
Bash & ShellCheck
Why Optimized?
The unoptimized image had the following issues:

Large Image Size: Installing multiple CLIs across several layers caused the image to become too large to run on public agents.
Inefficient Layering: Each RUN command creates a new layer, which can significantly increase image size if not handled properly.
Key Optimizations:
Layer Combining: Fewer RUN commands means fewer layers, reducing image size.
Cache Cleanup: Removal of apt and npm caches after installations to minimize bloat.
Multi-Stage Builds: Can be extended to include testing stages, ensuring only necessary dependencies are included in the final image.
