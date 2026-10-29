# Build a personal, interactive ShopMy closet

This is a brief for Claude, Codex, or another AI agent. Help the person build a website where each product in a closet scene opens its tracked ShopMy link. Explain choices in plain language and handle the code and files for them.

## 0. How this version works

- Every item opens the product's own tracked link from the person's ShopMy shelf, so clicks and commission still count.
- The header or a small label links to the full shelf.
- If the person prefers one link per shelf (category) instead, support that. Ask once. Never invent links or collection IDs. Never replace a missing link with a homepage.
- The scene is a vector (SVG) closet with the person's real product photos cut out and placed on shelves and hangers. It is one tall vertical scene so it fits a phone.

## 1. Ask before building

Ask a few related questions at a time. Skip anything already answered.

- Exact name and title wording, and which words should be biggest.
- Their ShopMy shelf link.
- The look: scene, mood, color, fonts, and anything to leave out.
- Inspiration photos and what they like about them.
- Where each item should go, or let the agent propose a layout.
- Phone first. Ask to show phone and desktop previews.

## 2. Get the products and tracked links

ShopMy pages are built with JavaScript, so a plain page fetch shows nothing.

1. Open the shelf in a real browser (a browser tool, or ask the person to paste the links).
2. List each product with brand and name.
3. Read each product's buy link (the Shop Now link). Use the link ShopMy provides for that product. Do not build links from product ids.
4. Links that go through `apiv3.shopmy.us/api/redirect_click` contain a `clickId`. Replace it with a fresh random UUID each time someone taps, so each click counts once. Leave other networks' links as they are.
5. Open links in a new tab with `rel="noopener sponsored"`.
6. Put the results in a table: label, brand, product, link, photo. Show it to the person before building.
7. Add a plain line on the page that the creator may earn a commission.

If the browser cannot read the links, ask the person to paste them. Do not guess.

## 3. Collect the photos

- Many retailer images cannot be downloaded or hotlinked by the agent. Ask the person to attach product photos.
- Say exactly which items need which photo type (see PERSONALIZE.md).
- Cut out each product from its background. Remove the background, keep the largest shape, fill small holes, crop tight, and view each cutout on a bright contrasting color before using it.
- Photos with a model in them do not hang well. Ask for a flat lay. If the person only has a model photo, a clean fabric patch can be reused as a texture on a drawn garment shape.
- If a photo is black and the real item is cream (or another color), recolor it by mapping brightness to a color ramp so the fabric texture stays.
- Do not make up product images. Do not use a generated image where exact appearance matters.

## 4. Design the scene

Show a plan and a mockup first. Keep the approved look. Do not redo the whole scene for a small fix.

Suggested closet layout (vertical, about 800 by 1500 units):

- Crown at the top with a small linked label.
- Two accessory shelves (glasses, clips, necklace on a stand, bags, beauty items).
- A gold rail with hanging pieces on gold hangers.
- A second gold rail for pants, clipped on a clip hanger.
- A bottom shelf with shoes and socks.
- A base cabinet and floor.

Design rules:

- Bright, clean, editorial. Thin lines, soft light, no clutter.
- Put light or gold items on a dark stand so they stand out.
- Give every item breathing room and center it in its box when asked.
- No extra props the person did not ask for.
- Fonts: an elegant serif for the name, a simple sans for body. Provide fallbacks.

## 5. Build the page

Use one simple HTML page. No server and no database.

- Inline SVG scene. Each item is an `<a>` around its image, with a `<title>`.
- Header with the name, a linked shelf label, and one line of instructions.
- Under or beside the scene, a list of every item with a thumbnail and brand and name. Hovering a list item highlights it in the scene.
- On a phone: one column, header first, then the scene, then the list.
- On a computer: two columns. Scene on the left and sticky, header and list on the right.
- Hover or focus glow, plus a small name tooltip. Do not rely on hover for touch. Respect reduced motion.
- Real links, clear accessible names, a visible keyboard focus, a page heading, and a skip to list link.
- Include a viewport meta tag.
- No analytics or add-ons unless asked.

## 6. Check it

- Screenshot at a phone width (390) and a desktop width (1360). Look at them.
- Check there is no sideways scrolling on a phone.
- Check every item opens the intended product link and every header link opens the shelf.
- Check the list works and the page reads well.
- Tell the person plainly what you could not test.

## 7. Publish on Vercel when asked

A direct request to publish is permission to publish. Never create accounts or type passwords. The person signs in.

1. Make a project folder with `index.html`, the images, and `vercel.json`:

```json
{
  "$schema": "https://openapi.vercel.sh/vercel.json",
  "framework": null,
  "buildCommand": null,
  "outputDirectory": "."
}
```

2. Create a new GitHub repository in the person's own account and add the files.
3. In Vercel, choose Add New, then Project, and import the repository.
4. Set Application Preset to Other, Root Directory to `./`, leave the build command empty, set Output Directory to `.`.
5. Click Deploy.
6. Copy the production address. Put it in the page's canonical link, `og:url`, and `og:image`. Commit again and wait for success.
7. Open the public link while logged out. Check phone and desktop. Give the person the link.

Later changes: update the files, commit to GitHub, wait for Vercel to finish, then confirm the live page.

## 8. Keep it honest

- This page opens existing links. It does not sync with ShopMy.
- Keep private references and credentials out of public repos.
- Use only photos and fonts the person is allowed to publish.
