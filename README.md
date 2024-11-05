# Understanding the Patterns of Project Ideas in 2023

See patterns in thousands of startup ideas!

Interactive visualization at: [https://build-space-visualization.vercel.app/](https://build-space-visualization.vercel.app/)

![CleanShot 2024-11-05 at 16 25 14@2x](https://github.com/user-attachments/assets/8efe60f3-2e47-47b1-848e-918613ead849)


At the start of each season of BuildSpace the program prompts thousands of participants to take up arms and flood social media feeds 
with the project they will be working on over the coming months. I collected and visualized them in an explorable way.

This is cool because you can see where young builders heads are at and see what is the public concious thinking about so you can differentiate yourself from everyone else. 

## Analytics

The scraped raw text alone doesn't mean very much. To identify patterns we have to group them. We can [use GPT to generate embeddings](https://platform.openai.com/docs/guides/embeddings) 
and then apply standard data analytics practices to these embeddings to numerically explore the generated space. 

Since some ideas were really short, embedding quality can be improved by using GPT to generate an extended description, extrapolating more text from the idea and therefore providing more context to the output embedding. (Each idea was fed to GPT who wrote a short ~1 paragraph description of the idea which was fed to the embedding request alongside the original text)

To generate labels for different themes of ideas, KMeans was used to generate groups of unlabeled points. Then, these aggregated groups titles and descriptions 
were all fed to GPT to generate an overarching title for the cluster. This was repeated for each group (25 groups) to generate the legend for the map.

For visualization's sake, we apply transformations to reduce dimensions into 2D the embeddings using TSNE in such a way that we maximize differentiation between "classes" of idea.

Also tried was LDA but since we don't require seperability (as would be in a classification problem) I wanted to preserve some everlap between the idea spaces rather than creating completely seperated clusters.


## Processing Scraped Content

We are provided the rare opportunity to peer at thousands of current startup/project ideas. 
If you're someone who is constantly brainstorming or thinking about future technology, you have no problem understanding why this is valuable. 

Scraping content is easy. During the Nights and Weekends launch, we search for all tweets and linkedin posts mentioning @_BuildSpace and filter by posts which contain image media.
Some manual removal is required of posts that don't contain ideas.

![bsideas](https://github.com/user-attachments/assets/43d2b00f-2c6b-4a3f-9d62-390cd0be8833)

The idea images provide a standardized templated image which we can extract text from. After some preprocessing (increasing contrast, crop, convert to black and white)
we feed the image to a python OCR script which is formatted into a csv. This is passed to our GPT analysis script.



