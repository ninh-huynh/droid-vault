## Free up space used by docker

We can check the space used by docker with the following command:

```powershell
docker system df

docker system df -v
```

Remove all thing we do not need anymore:
```powershell
docker system prune -a --volumes
```

Or remove individually
```powershell
docker container prune

docker network prune

docker image prune

docker volume prune
```

## Analyze the space used by distribution

```sh
du -h <Folder to analyze> | sort -rh | head -n 10
# Example for the root folder
du -h / | sort -rh | head -n 10

# Exclude the host machine disk on /mnt
du -h / --exclude /mnt | sort -rh | head -n 10
```

## Compat the WSL distribution

First stop the WSL
```powershell
wsl --shutdown
```


Then find the disk of the distribution

```powershell
cd C:\Users\%PROFILE%\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu20.04onWindows_79rhkp1fndgsc\LocalState\
```

We will see a file called **ext4.vhdx** that is the disk if the distribution. We will be able to verify that even after freeing up space within the distribution, the disk is still large.
To compat the disk we can use the following command

```powershell
optimize-vhd -Path .\ext4.vhdx -Mode full
```

