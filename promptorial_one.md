## Prompt: Initialize a new MiniKit project

```prompt
Create a new MiniKit project using the following command


npx create-onchain --mini


After running the command navigate into the new project directory and install the dependencies


cd [your-project-name]
npm install


refer to the following documentation to understand how MiniKit works:
https://docs.base.org/builderkits/minikit/llms.txt
https://docs.base.org/builderkits/onchainkit/llms.txt
```

## Prompt: Set up authentication and display user FID

```prompt
Create a client component at `components/AuthButton.tsx` that uses the `useAuthenticate` hook from MiniKit to handle user authentication and display the user's FID.

The component should:
- Be a client component (`'use client'`)
- Use `useAuthenticate` from `@coinbase/onchainkit/minikit`
- Show a login button if the user is not authenticated
- Show a message with the user's FID after successful authentication

Example:


'use client';

import { useState } from 'react';
import { useAuthenticate } from '@coinbase/onchainkit/minikit';

export default function AuthButton() {
  const [fid, setFid] = useState<number | null>(null);
  const { signIn } = useAuthenticate();

  const handleSignIn = async () => {
    const result = await signIn({
      domain: 'your-app.vercel.app', // 🔁 Replace with your actual domain
      siweUri: 'https://your-app.vercel.app/api/login',
    });

    if (result?.fid) {
      setFid(result.fid);
      console.log('Signed in FID:', result.fid);
    }
  };

  return !fid ? (
    <button
      onClick={handleSignIn}
      className="bg-black text-white px-4 py-2 rounded-2xl shadow"
    >
      Sign in with Farcaster
    </button>
  ) : (
    <p className="text-green-600 text-lg">✅ Signed in as FID: {fid}</p>
  );
}


Import this component in your `app/page.tsx` file.

Create a minimal API route at `app/api/login/route.ts` using `verifySignInMessage`:


import { verifySignInMessage } from '@farcaster/auth-kit';
import { NextResponse } from 'next/server';

export async function POST(req: Request) {
  const { message, signature } = await req.json();

  try {
    const { fid } = await verifySignInMessage(message, signature);
    return NextResponse.json({ fid });
  } catch {
    return NextResponse.json({ error: 'Invalid signature' }, { status: 401 });
  }
}
```

## Prompt: Show user identity card after authentication

```prompt
Update your `app/page.tsx` file to conditionally render content based on the user's authenticated state.

Import and render the existing `AuthButton` component at the top of the page. Only display the main content after the user has authenticated (i.e., has a valid FID).

Then, create a new component at `components/IdentityCard.tsx` that accepts a `username` and `pfp` as props and displays the user's identity.

The IdentityCard should:
- Accept `username: string` and `pfp: string`
- Display the user's profile picture and username
- Use basic Tailwind styling

Example `IdentityCard.tsx`:


'use client';

type IdentityCardProps = {
  username: string;
  pfp: string;
};

export default function IdentityCard({ username, pfp }: IdentityCardProps) {
  return (
    <div className="flex items-center gap-4 p-4 rounded-xl shadow bg-white">
      <img src={pfp} alt="pfp" className="w-12 h-12 rounded-full" />
      <p className="text-lg font-semibold">@{username}</p>
    </div>
  );
}


Then in `app/page.tsx`, render the `IdentityCard` after the user has signed in:

'use client';

import { useState } from 'react';
import AuthButton from '@/components/AuthButton';
import IdentityCard from '@/components/IdentityCard';

export default function HomePage() {
  const [user, setUser] = useState<{ username: string; pfp: string } | null>(null);

  return (
    <main className="p-8">
      <AuthButton onAuthSuccess={setUser} />
      {user && <IdentityCard username={user.username} pfp={user.pfp} />}
    </main>
  );
}


Pass a callback prop (`onAuthSuccess`) to `AuthButton` that is triggered after a successful sign-in, passing the user's `username` and `pfp`. Store this in local state and use it to render the identity card.

Only authenticated users will see the identity content.
```

## Prompt: Deploy your MiniKit app to Vercel

```prompt
Deploy your MiniKit app to Vercel using the following steps:

1. Install the Vercel CLI globally (if not already installed):


npm install -g vercel

In your MiniKit project root, run the deployment command:

After deployment completes, you'll receive a live URL like:

Update your MiniKit AuthButton.tsx logic to use your live domain. Replace the domain and siweUri values in signIn():

const result = await signIn({
  domain: 'your-app-name.vercel.app', //  Replace with your actual Vercel domain
  siweUri: 'https://your-app-name.vercel.app/api/login',
});
```

## Prompt: Generating manifest

```prompt
npx create-onchain --manifest
```