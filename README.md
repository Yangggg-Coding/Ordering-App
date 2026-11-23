# Coffee Ordering App

A full stack coffee shop ordering app. Customers browse the menu, add drinks to a cart, sign in, and place an order. Orders are saved in a database, and each customer can see their order history.

Built with React, JavaScript, CSS, and Supabase.

![Ordering app screenshot](./docs/screenshot.png)

**Live demo:** add your link after you deploy.

## Features

Tick each box when the feature works.

- [ ] Menu loaded from the database, with categories and search
- [ ] Item page with size and extras options
- [ ] Cart with quantity, remove, and total price
- [ ] Cart saved in localStorage
- [ ] Sign up, log in, and log out
- [ ] Protected checkout and order history pages
- [ ] Place an order and save it in the database
- [ ] Order status: pending, preparing, ready
- [ ] Loading, error, and empty states
- [ ] Responsive layout for phone and desktop

## Tech stack

| Area | Tool |
|---|---|
| UI | React, JavaScript |
| Styling | Plain CSS with variables |
| Routing | React Router |
| Backend and database | Supabase (PostgreSQL, Auth) |
| Build tool | Vite |
| Linting | ESLint |

## Getting started

Needs Node.js 18 or newer and a free Supabase project.

```bash
git clone https://github.com/Yangggg-Coding/ordering-app.git
cd ordering-app
npm install
```

Create a `.env` file in the project root:

```
VITE_SUPABASE_URL=your-project-url
VITE_SUPABASE_ANON_KEY=your-anon-key
```

Then start the app:

```bash
npm run dev
```

Other scripts: `npm run build`, `npm run preview`, `npm run lint`.

Never commit the `.env` file. Keep it in `.gitignore`.

## Project structure

```
src/
  components/    # Navbar, MenuItemCard, CartItem, OrderCard, Loader, ErrorMessage
  pages/         # Home, Menu, ItemDetail, Cart, Checkout, Orders, Login, NotFound
  context/       # AuthContext, CartContext
  hooks/         # useMenu, useOrders
  services/      # supabaseClient, menuApi, orderApi
  utils/         # formatters
  App.jsx  main.jsx  index.css
```

## Routes

| Path | Page | Access |
|---|---|---|
| `/` | Home | Public |
| `/menu` | Menu | Public |
| `/menu/:id` | Item detail | Public |
| `/cart` | Cart | Public |
| `/login` | Log in and sign up | Public |
| `/checkout` | Checkout | Logged in |
| `/orders` | Order history | Logged in |
| `*` | Not found | Public |

## Database

| Table | Main columns |
|---|---|
| `menu_items` | id, name, description, category, price, image, available |
| `orders` | id, user_id, status, total, created_at |
| `order_items` | id, order_id, menu_item_id, size, quantity, unit_price |

Row Level Security is on. Anyone can read `menu_items`. A user can read and create only their own `orders` and `order_items`.

## How it works

- `menuApi` loads the menu, and `useMenu` returns `items`, `loading`, and `error`.
- `CartContext` holds the cart and saves it in localStorage.
- `AuthContext` holds the signed-in user from Supabase Auth.
- A protected route sends logged-out visitors to `/login`.
- At checkout, `orderApi` saves one `orders` row and its `order_items` rows. The server stores the price, so a visitor cannot change it.

## AI as an assistant

I used an AI assistant (Claude by Anthropic) as a learning aid and pair programmer. I stayed in charge of the design, the code, and every decision.

- **AI:** explained concepts, suggested the structure and database tables, reviewed my code, and explained bugs.
- **Me:** designed the screens, wrote and tested the code, set up the database, fixed errors, and checked each change with `npm run lint`.

## Roadmap

1. Finish the features above
2. Add an admin page to update order status
3. Add online payment with a test mode
4. Add tests for the cart logic
5. Deploy to Vercel

## Author

Heang Hongyang. GitHub: [Yangggg-Coding](https://github.com/Yangggg-Coding)

## License

MIT. Add a `LICENSE` file before you publish.
