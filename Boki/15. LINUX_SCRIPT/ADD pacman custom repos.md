To add multiple custom repositories to the Pacman configuration file (`/etc/pacman.conf`), you can use a script that appends the repository information to the end of the configuration file. Here's a simple bash script to achieve this:

```
#!/bin/bash 

# Function to add a custom repository to pacman.conf add_repository() { 
repo_name="$1" 
repo_url="$2" 

echo -e "\n[${repo_name}]\nSigLevel = Optional TrustAll\nServer = ${repo_url}\n" | sudo tee -a /etc/pacman.conf } 

# Add your custom repositories here 
# Example: 
# add_repository "my_repo" "https://example.com/repo" 

# Uncomment and edit the lines below to add your custom repositories 
# add_repository "custom_repo_1" "https://custom_repo_1_url" 
# add_repository "custom_repo_2" "https://custom_repo_2_url" 
# add_repository "custom_repo_3" "https://custom_repo_3_url" 
# https://gitlab.com/bojanstrkovski-21/\$repo/-/raw/main/\$arch/

# After adding the repositories, you may want to refresh the package database 

# sudo pacman -Sy 

echo "Custom repositories added to pacman.conf."
```




Replace the example URLs with the actual URLs of your custom repositories. Save the script to a file (e.g., `add_custom_repos.sh`), and then make the script executable:

```
chmod +x add_custom_repos.sh
```


To run the script and add the custom repositories to `pacman.conf`, execute the following command:


```
./add_custom_repos.sh
```

Please make sure to review the URLs and ensure that you trust the sources before adding them to your Pacman configuration. Adding untrusted or unknown repositories can compromise the security and stability of your system. Always use caution when adding custom repositories.