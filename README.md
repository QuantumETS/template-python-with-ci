# Template Python + CI pour Quantum ÉTS

Ce dépôt sert de **base de départ minimale** pour les projets Python du club, en particulier pour les membres débutants ou intermédiaires.

Il est pensé pour deux cas fréquents:

1. Hackathon avec sujet déterminé, mais sans code fourni: vous pouvez partir de ce template et développez votre code/tests à partir de zéro.
2. Hackathon avec dépôt de départ fourni: vous réutilisez la structure CI/tests de ce template et ajoutez les documents, codes et dépendances spécifiques au projet.

>[!NOTE]
> Dans le cas d'un hackathon avec dépôt de départ fourni, il vaudra peut-être mieux utiliser un autre template agnostique des outils de développement (pytest, pre-commit, etc.) pour éviter les conflits de configuration. Par exemple, un template avec des instructions pour des agents sera peut-être plus adapté.

Ce template est conçu pour être utilisé comme **template GitHub d'organisation** afin de créer rapidement de nouveaux dépôts cohérents au sein du club.

## Ce que contient ce template

- `src/`: code source Python, où se trouve le code d'application.
- `tests/`: tests unitaires, suivant la convention ["src layout"](https://docs.pytest.org/en/stable/explanation/goodpractices.html#tests-outside-application-code).
- `.github/workflows/unit-tests.yml`: exécution automatique des tests sur GitHub Actions.
- `requirements-test.txt`: dépendances nécessaires aux tests.
- `requirements-dev.txt`: dépendances pour le développement, outils de qualité statique, etc.
- `.pre-commit-config.yaml`: configuration des hooks `pre-commit` (Black).

L'exemple de code est volontairement minimal (`sum`) pour rester lisible et servir de squelette.

## Outils et standard d'équipe

- **GitHub Actions** (`.github/workflows/unit-tests.yml`): exécute automatiquement les tests à chaque push/PR pour garantir que tout le monde valide le même niveau de qualité avant fusion.
- **pytest** (`requirements-test.txt`): framework de tests unitaires, utilisé pour vérifier le comportement du code de manière reproductible entre les membres.
- **pre-commit** (`requirements-dev.txt` + `.pre-commit-config.yaml`): au moment de commit, l'outil `pre_commit` exécute les hooks configurés, pour garantir que le code respecte les standards de qualité avant même d'être poussé.
- **Black** (hook via `pre-commit`): formateur de code Python qui impose un style unique conforme au standard [PEP 8](https://www.python.org/dev/peps/pep-0008/), pour éviter les débats de style et garder un code lisible et uniforme. Il existe une extension VSCode pour l'exécuter automatiquement à chaque sauvegarde, vous évitant un échec du pre-commit à cause du formatage.
- **Séparation des dépendances** (`requirements-test.txt` / `requirements-dev.txt`): distingue les dépendances nécessaires pour exécuter les tests de celles nécessaire pour le développement, en plus d'être distinctes du fichier habituel `requirements.txt` qui pourrait être utilisé pour les dépendances de l'application ou du hackathon.

## Première configuration

> [!IMPORTANT]
> Ce template est prévu pour `pip` avec `venv` ou `conda`. Si vous utilisez `uv`, ce template n'est pas approprié.

### Configuration avec [`venv`](https://docs.python.org/3/library/venv.html#creating-virtual-environments)

<details>
<summary>Instructions pour venv</summary>

#### 1) Créer et activer l'environnement

Windows (PowerShell):

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

macOS / Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

#### 2) Installer les dépendances

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements-test.txt
python -m pip install -r requirements-dev.txt
```

#### 3) Exécuter les tests

```bash
python -m pytest tests/
```

#### 4) Installer et lancer les hooks qualité

```bash
python -m pre_commit install
python -m pre_commit run --all-files
```

</details>

### Configuration avec [`conda`](https://docs.conda.io/projects/conda/en/stable/user-guide/getting-started.html)

<details>
<summary>Instructions pour conda</summary>

#### 1) Créer et activer l'environnement

```bash
conda create -n mon_environnement python=3.14 -y
conda activate mon_environnement
```

#### 2) Installer les dépendances

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements-test.txt
python -m pip install -r requirements-dev.txt
```

#### 3) Exécuter les tests

```bash
python -m pytest tests/
```

#### 4) Installer et lancer les hooks qualité

```bash
python -m pre_commit install
python -m pre_commit run --all-files
```

</details>

## Usage courant

- **Développement**: travaillez dans `src/` pour le code d'application, et dans `tests/` pour les tests unitaires.
- **Tests**: lancez les tests avec pytest (`python -m pytest tests/`) pour vérifier que votre code fonctionne comme prévu.
- **Qualité**: les hooks `pre-commit` s'exécutent automatiquement au moment du commit.
- **CI**: à chaque push sur `main` ou `dev`, et à chaque Pull Request, les tests sont exécutés automatiquement sur GitHub Actions pour garantir que le code fusionné passe les tests.
- **Documentation**: ajoutez des commentaires et des docstrings (Google Style) pour expliquer le fonctionnement de votre code, surtout si vous travaillez en équipe.
- **Type-hints**: utilisez des annotations de type pour faciliter la lecture par les pairs et l'IA si vous en utilisez.

**Puis-je utiliser uv ?**

Comme `uv` gère l'environnement et les dépendances à l'aide d'un groupe de fichiers de configuration (`uv.lock`, `pyproject.toml`), et que ces fichiers ne sont pas présents dans ce template, il est recommandé d'utiliser `venv` ou `conda`.

## Ressources supplémentaires

### Outils de développement

- [Documentation pytest](https://docs.pytest.org/en/stable/)
- [Documentation pre-commit](https://pre-commit.com/)
- [Documentation Black](https://black.readthedocs.io/en/stable/)
- [Documentation pre-commit Black hook](https://github.com/psf/black-pre-commit-mirror)
- [PEP 8 - Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/)

### Gestion d'environnement

- [venv - Python documentation](https://docs.python.org/3/library/venv.html)
- [conda - Documentation](https://docs.conda.io/projects/conda/en/stable/user-guide/getting-started.html)
