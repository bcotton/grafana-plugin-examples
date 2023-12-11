load('ext://configmap', 'configmap_create')

# Tell ops-devenv/Tiltifle where our plugin.json file lives
plugin_file = os.path.abspath('examples/app-with-backend/src/plugin.json')
def plugin_json():
    return plugin_file

local_resource('example frontend', cmd='cd examples/app-with-backend; yarn install', serve_cmd='cd examples/app-with-backend; yarn dev')

local_resource('example backend', cmd='cd examples/app-with-backend && which mage && mage -v')


configmap_create('myorg-withbackend-app-provisioning',
				  
				  namespace='default',
				  from_file='examples/app-with-backend/provisioning/plugins/myorg-withbackend-app-provisioning.yaml')

k8s_resource(objects=['myorg-withbackend-app-provisioning:configmap'],
    		new_name='myorg-withbackend-app-provisioning-configmap',
			resource_deps = ['example frontend', 'example backend'],
			labels=['Grafana'])
