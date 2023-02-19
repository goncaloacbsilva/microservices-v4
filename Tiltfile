# A list of apps located in /apps that we need to build images for
apps = ['service-1', 'service-2']

sync_source = sync('.', '/app');
install_deps = run('yarn install', trigger='package.json')

# This function will define a docker build step for the provided application.
def build_app(name):
    image_name = 'gxspace/{}'.format(name)
    context = '.'
    dockerfile = './apps/{}/Dockerfile'.format(name)

    docker_build(image_name, context, dockerfile=dockerfile, live_update=[sync_source, install_deps])

def deploy_app(name):
    deployment = './apps/{}/deploy.yml'.format(name)
    k8s_yaml(deployment)

# Build the base image that includes node_modules and source code
docker_build('gxspace/svc-base', '.')

# Build image for each application
[build_app(name) for name in apps]

# Deploy services
[deploy_app(name) for name in apps]

# Apply Istio Gateway Ingress

k8s_yaml('IstioGateway.yml')

