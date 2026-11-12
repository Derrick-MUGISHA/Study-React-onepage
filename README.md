# Forma — React props, state, and events

A responsive learning community page built with React and Vite. Includes a mobile menu, course filters, save buttons, a testimonial carousel, and a controlled signup form. All content is sample data; signup is a local demo and does not send or store emails. Photos load from Unsplash, with a bundled illustration if the network is unavailable.

## Run locally

```sh
npm install
npm run dev
```

Create a production build with `npm run build`. Run static checks with `npm run lint`.

## Where to start studying

1. **`src/component/data.js`**: change a title, add a course, or add a testimonial. This is ordinary JavaScript data, separate from presentation.
2. **`src/App.jsx`**: study `useState`. App owns the values and passes them down through props.
3. **`src/component/CourseCard.jsx`**: `course` and `isSaved` are data props. `onSave` is a callback prop. Clicking the button calls `onSave(course.id)`.
4. **`src/component/Courses.jsx`**: `.filter()` chooses courses and `.map()` renders reusable cards with stable keys. Props flow from App to Courses to CourseCard.
5. **`src/component/Testimony.jsx`**: `activeIndex` selects a testimonial, and `onChange` asks App to update that state. Previous/next buttons wrap around the list.
6. **`src/component/Newsletter.jsx`**: `value={email}` and `onChange` make a controlled input. The form passes its submit event to App, which uses `preventDefault()` and displays local feedback.
7. **Navigation, Hero, Footer**: each receives its content through props too. Not every component needs its own state; state lives in App so related components can share it.

## Follow a click

```text
CourseCard: click Save → onSave(course.id)
App: handleSave(id) → setSavedIds(previous => ...)
React renders again → new isSaved prop reaches CourseCard
Navigation receives the updated savedCount prop
```

Use `onClick={() => onSave(course.id)}` to pass a function that runs later. Writing `onClick={onSave(course.id)}` would call it while rendering.

State updates based on the previous value use the functional form (`setSavedIds(previous => ...)`). Arrays are replaced with new arrays using spread and filter; they are never mutated.

## Practice exercises

- Add a course to `data.js` and see it appear without changing CourseCard.
- Add a new category to both a course and `categories`.
- Add a saved-only filter using `savedIds.includes(course.id)`.
- Add a `likes` state and pass `likes` and `onLike` props to a new component.
- Move menu state inside Navigation, then compare local state with the shared state in App.

The folder keeps the original project name `src/component` to preserve existing import paths. Saved courses and form feedback reset on refresh.
