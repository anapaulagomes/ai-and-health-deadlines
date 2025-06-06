---
title: AI Deadlines
emoji: ⚡
colorFrom: gray
colorTo: green
sdk: docker
pinned: false
app_port: 8080
---

# AI Conference Deadlines

A web app to quickly see submission deadlines to top AI conferences, such as NeurIPS and ICLR.

## Project info

This project is entirely based on the awesome https://github.com/paperswithcode/ai-deadlines. As that repository is no longer maintained, we decided to make an up-to-date version along with a new UI. It was bootstrapped using [Lovable](https://lovable.dev/) and [Cursor](https://www.cursor.com/).

New data is fetched from https://github.com/ccfddl/ccf-deadlines/tree/main/conference/AI thanks to [this comment](https://github.com/paperswithcode/ai-deadlines/issues/723#issuecomment-2603420945). 

A CRON job (set up as a [Github action](.github/workflows/update-conferences.yml)) automatically updates the data present at src/data/conferences.yml.

**URL**: https://ai-and-health-deadlines.fly.dev/

## Contribute

Contributions are very welcome!

To keep things minimal, we mainly focus on top-tier conferences in AI and Healthcare.

To add or update a deadline:
- Fork the repository
- Update [src/data/conferences.yml](src/data/conferences.yml)
- Make sure it has the `title`, `year`, `id`, `link`, `deadline`, `timezone`, `date`, `city`, `country`, `tags` attributes
    + See available timezone strings [here](https://momentjs.com/timezone/).
- Optionally add a `venue`, `note` and `abstract_deadline` in case this info is known
- Optionally add `hindex` (refers to h5-index from [here](https://scholar.google.com/citations?view_op=top_venues&vq=eng))
- Example:
    ```yaml
    - title: BestConf
      year: 2022
      id: bestconf22  # title as lower case + last two digits of year
      full_name: Best Conference for Anything  # full conference name
      link: link-to-website.com
      deadline: YYYY-MM-DD HH:SS
      abstract_deadline: YYYY-MM-DD HH:SS
      timezone: Asia/Seoul
      city: Incheon
      country: South Korea
      venue: Incheon Conference Centre, South Korea
      date: September, 18-22, 2022
      start: YYYY-MM-DD
      end: YYYY-MM-DD
      paperslink: link-to-full-paper-list.com
      pwclink: link-to-papers-with-code.com
      hindex: 100.0
      tags:
      - machine learning
      note: Important
    ```
- Send a pull request to update [src/data/conferences.yml](src/data/conferences.yml).

## How to run locally

If you want to work locally using your own IDE, you can clone this repo and push changes.

The only requirement is having Node.js & npm installed - [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating)

Follow these steps:

```sh
# Step 1: Clone the repository using the project's Git URL.
git clone https://github.com/huggingface/ai-deadlines

# Step 2: Navigate to the project directory.
cd ai-deadlines

# Step 3: Install the necessary dependencies.
npm i

# Step 4: Start the development server with auto-reloading and an instant preview.
npm run dev
```

This runs the app at http://localhost:8080/.

## Deploy with Docker

First build the Docker image as follows:

```bash
docker build -t ai-deadlines .
```

Next it can be run as follows:

```bash
docker run -it -p 8080:8080 ai-deadlines
```

You can see it in your web browser at http://localhost:8080/.

## Deploy on the cloud

One way to deploy this on a cloud is by using [Artifact Registry](https://cloud.google.com/artifact-registry/docs) (for hosting the Docker image) and [Cloud Run](https://cloud.google.com/run?hl=en) (a serverless service by Google to run Docker containers). See [this YouTube video](https://youtu.be/cw34KMPSt4k?si=UbzNRobNzib93uDl) for a nice intro.

Make sure to:
- create a [Google Cloud project](https://console.cloud.google.com/)
- set up a billing account
- have the [gcloud SDK installed](https://cloud.google.com/sdk/docs/install).

To deploy, simply run:

```bash
gcloud auth login
gcloud auth application-default login
gcloud run deploy --source .
```

## Technologies used

This project is built with:

- Vite
- TypeScript
- React
- shadcn-ui
- Tailwind CSS

## License

This project is licensed under [MIT](LICENSE).

## Maintainers

Feel free to just open an issue. Otherwise contact @nielsrogge
