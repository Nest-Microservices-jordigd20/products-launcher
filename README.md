# Products launcher

## Development environment

1. Clonate the repository
2. Install the dependencies
3. Run the following command to rebuild the submodules

```bash
git submodule update --init --recursive
```

4. Create a `.env` based on the `.env.template` file.
5. Run the following command:

```bash
$ docker compose up --build
```

## Git Submodules

1. To add a submodule, run the following command, where `<repository_url>` is the URL of the repository you want to add and `<directory_name>` is the name of the directory where the repository will be cloned. (The directory must not exist)

```bash
git submodule add <repository_url> <directory_name>
```

2. Add the changes to the repository

```bash
git add .
git commit -m "Add <directory_name> submodule"
git push
```

3. When someone clones the repository for the first time, they will have to run the following command to initialize and update the submodules

```bash
git submodule update --init --recursive
```

4. To update the submodules references

```bash
git submodule update --remote
```

### Important

If you are working in the submodule repository, you should first **update and push** the changes in the submodule and **then** update the changes in the main repository.

If you do it the other way around, you will lose the references of the submodules in the main repository and you will have to resolve conflicts.
