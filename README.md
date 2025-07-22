# Smash Rankings

Simple Vue webpage displaying Super Smash Bros. Ultimate player rankings.

## Usage

#### Docker

```
docker build -t smash-rankings .
docker run -p 8080:80 smash-rankings
```

#### Npm

```
npm install
npm run dev
```

or compile/minify for production

```
npm run build
```

## Configuration

Player data is located in `public/data.json`. All available icons are located in `public/ssbuicons/`.
