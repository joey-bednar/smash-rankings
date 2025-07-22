# Smash Rankings

Simple Vue webpage displaying Super Smash Bros. Ultimate player rankings.

## Usage

#### Docker

```
docker build -t smash-rankings .
docker run -p 8080:80 smash-rankings
```

Open `localhost:8080` in a web browser to view.

#### Npm

```
npm install
npm run dev
```

Open `localhost:5173` in a web browser to view.

or compile/minify for production

```
npm run build
```

## Configuration

Player data is located in `public/data.json`. All available icons are located in `public/ssbuicons/`.
