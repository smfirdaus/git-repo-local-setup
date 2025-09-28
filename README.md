# Github local repo setup (MacOS)

## Create the Repo
1. Go to GitHub → Create a new repo named smfirdaus.github.io 
- Public repo.
- No template for now.

2. Clone it to your MacBook:
```
git clone https://github.com/smfirdaus/smfirdaus.github.io.git
cd smfirdaus.github.io
```

## Add al-folio theme
1. Clone the al-folio repository to local machine.
```
git clone https://github.com/alshedivat/al-folio.git temp-folio
cp -r temp-folio/* temp-folio/.* ./   # copy into your repo
rm -rf temp-folio
```
2. Install dependencies:
`bundle install`

- Since al-folio supports jupyter notebooks, we also need to install it. If you are not planning to use notebooks that much, you can install it via pipx. To install both pipx and jupyter, run the following commands:
```
python3 -m pip install --user pipx
python3 -m pipx ensurepath
pipx install jupyter --include-deps
pipx ensurepath
```

3. If receive error "sh: convert: command not found", this indicates that the convert command, which is part of ImageMagick, is not found in system's PATH. This means Jekyll cannot locate the ImageMagick utility it needs to process images.
- Install ImageMagick:
`brew install imagemagick`
- Verify that the convert command is now available in your PATH by running:
`which convert`

## Build and serve al-folio locally
Open the al-folio directory and call Jekyll:
bundle exec jekyll serve

## Reference:
1. https://george-gca.github.io/blog/2022/running-local-al-folio/
2. https://github.com/alshedivat/al-folio/blob/main/INSTALL.md
