# Github repository local setup (MacOS)

## 1. Create the Repo
1. Go to GitHub → Create a new repo named smfirdaus.github.io 
- Public repo.
- No template for now.

2. Clone it to your MacBook:
```
git clone https://github.com/smfirdaus/smfirdaus.github.io.git
cd smfirdaus.github.io
```

## 2. Add al-folio theme
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

## 3. Build and serve al-folio locally
1. Open the al-folio directory and call Jekyll:
`bundle exec jekyll serve`

2. Now open http://localhost:4000 → you should see al-folio theme running locally.

## 4. Push to GitHub
1. Once it works locally:
```
git add .
git commit -m "Set up al-folio theme"
git push origin main
```

2. GitHub Pages will build automatically.  
Check: https://smfirdaus.github.io

## 5. Plan for Sub-Sites (/docs, /blog)
Since GitHub Pages only builds one Jekyll site per repo, you have two options:  

#### ✅ Option A (Simpler for You):  
- Keep al-folio as the main site.
- For /docs and /blog, you pre-build them locally and copy the static output (_site) into /docs and /blog folders in your main repo.
- Example structure:  
```
  smfirdaus.github.io/
│
├── _config.yml        # al-folio config
├── index.md           # homepage
│
├── docs/              # built static HTML for docs site
│   └── index.html
│
└── blog/              # built static HTML for blog site
    └── index.html
```
To do:  
1.	Create another Jekyll site in ~/projects/docs-site/.
2.	Run bundle exec jekyll build.
3.	Copy the _site output into /docs in your main repo.
4.	Commit and push.

GitHub will serve it at https://smfirdaus.github.io/docs.

#### ✅ Option B (More Advanced):
- Use GitHub Actions to automatically build /docs and /blog from source.
- This requires setting up workflows (like I showed earlier).

## 6. Add Docs/Blog Later
1.	Create a Jekyll site for docs:
```
jekyll new docs-site
cd docs-site
bundle install
bundle exec jekyll build -d ../smfirdaus.github.io/docs
```
2.	Do the same for blog:
```
jekyll new blog-site
cd blog-site
bundle install
bundle exec jekyll build -d ../smfirdaus.github.io/blog
```
3.	Push changes:
```
cd ../smfirdaus.github.io
git add .
git commit -m "Add docs and blog sub-sites"
git push origin main
```
4. Final web structure:
- Main site → https://smfirdaus.github.io
- Docs site → https://smfirdaus.github.io/docs
- Blog site → https://smfirdaus.github.io/blog


## 7. Reference:
1. https://george-gca.github.io/blog/2022/running-local-al-folio/
2. https://github.com/alshedivat/al-folio/blob/main/INSTALL.md
