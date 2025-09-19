# occ - OpenShift Console wrapper for oc command

`occ` is a transparent wrapper around the `oc` command that enhances your OpenShift CLI experience by showing relevant console URLs on stderr while executing your commands.

## Features

- Acts as a transparent wrapper around `oc` - all commands work exactly the same
- Shows relevant OpenShift console URLs for your commands
- **Enhanced resource detection** - Automatically detects resource types, API groups, and versions using `oc api-resources`
- **Namespace-aware URLs** - Generates appropriate console URLs for both namespaced and cluster-scoped resources
- **Comprehensive resource support** - Built-in support for core Kubernetes resources plus dynamic detection for custom resources
- **Improved explain command** - Links directly to OpenShift console API resource schema for interactive documentation
- Supports autocomplete just like the original `oc` command
- Zero configuration required - works with your existing OpenShift setup

## Installation

1. Download the `occ` script to a directory in your PATH:
```bash
curl -o /usr/local/bin/occ https://raw.githubusercontent.com/wingsuitist/occ/main/occ
chmod +x /usr/local/bin/occ
```

2. Or clone this repository and copy the script:
```bash
git clone https://github.com/wingsuitist/occ.git
cd occ
cp occ /usr/local/bin/occ
chmod +x /usr/local/bin/occ
```

## Enable Autocomplete

First, ensure `oc` completion is set up for your shell:

### Bash
Add to your `.bashrc` or `.bash_profile`:

```bash
source <(oc completion bash)
complete -F __start_oc occ
```

Then reload your shell configuration:
```bash
source ~/.bashrc
```

### Zsh
Add to your `.zshrc`:

```bash
source <(oc completion zsh)
compdef _oc occ
```

Then reload your shell configuration:
```bash
source ~/.zshrc
```

## Usage

Use `occ` exactly like you would use `oc`:

```bash
# List pods and see console URL
occ get pods

# Describe a deployment with direct console link to my-app
occ describe deployment my-app

# Get help with documentation links
occ explain pod.spec.containers

# Any oc command works
occ logs my-pod
occ apply -f deployment.yaml
```

## Examples

When you run commands, you'll see console URLs on stderr (shown with 🌐):

```bash
$ occ get pods
🌐 https://console-openshift-console.apps.cluster.example.com/k8s/ns/my-namespace/core~v1~Pod
NAME                     READY   STATUS    RESTARTS   AGE
my-app-7d4b8c8f9-xyz12   1/1     Running   0          5m
```

```bash
$ occ explain pod.spec
🌐 https://console-openshift-console.apps.cluster.example.com/api-resource/ns/my-namespace/core~v1~Pod/schema
# ... explanation output
```

## Requirements

- OpenShift CLI (`oc`) must be installed and configured
- Active connection to an OpenShift cluster
- Bash shell

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Warning

⚠️ **DISCLAIMER**: This software is provided "as is" without warranty of any kind, express or implied. There is no guarantee that this software will work correctly, be secure, or be suitable for any particular purpose. Use at your own risk.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
## @TODO: Rewrite in Go 🤪

```
         ,_---~~~~~----._         
  _,,_,*^____      _____``*g*\"*, 
 / __/ /'     ^.  /      \ ^@q   f 
[  @f | @))    |  | @))   l  0 _/  
 \`/   \~____ / __ \_____/    \   
  |           _l__l_           I   
  }          [______]           I  
  ]            | | |            |  
  ]             ~ ~             |  
  |                            |   
   |                           |   
@ProggerX
```
