
# MiniKit Mini App Development Promptorial

## Prompt 1: Project Scaffolding
```
Create a new MiniKit project using the create-onchain CLI. Follow these exact steps:

1. Run the scaffolding command:
npx create-onchain@alpha --mini my-mini-app

2. Navigate into the project directory:
cd my-mini-app

3. Install dependencies:
npm install

Verify the project structure has been created successfully. Confirm you see:
- /src directory
- page.tsx file
- package.json
- Next.js configuration files
```

## Prompt 2: Clean Project Setup
```
Remove the default Snake component to prepare for custom implementation:

1. Open /src/app/page.tsx
2. Replace ALL existing code with a minimal React component:

'use client';
import React from 'react';

export default function HomePage() {
  return (
    <div>
      <h1>My MiniKit Mini App</h1>
    </div>
  );
}
```

## Prompt 3: Authentication Setup
```
Implement Farcaster wallet authentication using MiniKit's hooks:

1. Import necessary hooks:
import { useAuthenticate, useFarcasterContext } from 'minikit';
import { useState } from 'react';

2. Create authentication handler in page.tsx:
export default function HomePage() {
  const { signIn } = useAuthenticate();
  const context = useFarcasterContext();
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  const handleSignIn = async () => {
    const result = await signIn({
      domain: process.env.NEXT_PUBLIC_APP_DOMAIN,
      siweUri: `${process.env.NEXT_PUBLIC_APP_URL}/login`
    });

    if (result) {
      setIsLoggedIn(true);
      console.log('Authentication successful');
    }
  };

  return (
    <div>
      {!isLoggedIn ? (
        <button onClick={handleSignIn}>
          Login with Farcaster
        </button>
      ) : (
        <div>
          <h1>Welcome, {context?.user?.username}!</h1>
        </div>
      )}
    </div>
  );
}
```

## Prompt 4: First Login Confetti
```
Add a celebratory confetti effect for new users:

1. Install react-confetti:
npm install react-confetti

2. Update page.tsx to include confetti:
import Confetti from 'react-confetti';

export default function HomePage() {
  // ... previous authentication code

  return (
    <div>
      {!isLoggedIn ? (
        <button onClick={handleSignIn}>
          Login with Farcaster
        </button>
      ) : (
        <div>
          {context?.user?.isNewUser && <Confetti />}
          <h1>Welcome, {context?.user?.username}!</h1>
        </div>
      )}
    </div>
  );
}
```

## Prompt 5: Manifest Configuration
```
Prepare manifest.json for Vercel deployment:

Create /public/manifest.json with:
{
  "name": "My Mini App",
  "description": "A MiniKit Mini App with Farcaster authentication",
  "icons": [
    {
      "src": "/icon.png",
      "sizes": "192x192",
      "type": "image/png"
    }
  ]
}

Ensure you have a 192x192 icon in /public/icon.png
```

## Prompt 6: Vercel Deployment
```
Deploy to Vercel:

1. Ensure you have Vercel CLI installed:
npm install -g vercel

2. Login to Vercel:
vercel login

3. Deploy the project:
vercel

4. Set environment variables in Vercel dashboard:
- NEXT_PUBLIC_APP_DOMAIN
- NEXT_PUBLIC_APP_URL
- FARCASTER_MNEMONIC (if required)

Verify deployment URL and test Farcaster login
```

## Final Verification Prompt
```
Conduct a comprehensive test of your MiniKit Mini App:

1. Verify login button appears
2. Click login and complete Farcaster authentication
3. Confirm username displays after login
4. Check if confetti appears for new users
5. Ensure smooth navigation and error handling
```

This promptorial provides a step-by-step guide to building a MiniKit Mini App with Farcaster authentication, deployed on Vercel, complete with a welcoming user experience.
Preview
Text
I'll help you create a comprehensive prompt guide for building a MiniKit Mini App. I'll structure this as a series of precise, actionable prompts that a developer can follow step-by-step.

# MiniKit Mini App Development Promptorial

## Prompt 1: Project Scaffolding
```
Create a new MiniKit project using the create-onchain CLI. Follow these exact steps:

1. Run the scaffolding command:
npx create-onchain@alpha --mini my-mini-app

2. Navigate into the project directory:
cd my-mini-app

3. Install dependencies:
npm install

Verify the project structure has been created successfully. Confirm you see:
- /src directory
- page.tsx file
- package.json
- Next.js configuration files
```

## Prompt 2: Clean Project Setup
```
Remove the default Snake component to prepare for custom implementation:

1. Open /src/app/page.tsx
2. Replace ALL existing code with a minimal React component:

'use client';
import React from 'react';

export default function HomePage() {
  return (
    <div>
      <h1>My MiniKit Mini App</h1>
    </div>
  );
}
```

## Prompt 3: Authentication Setup
```
Implement Farcaster wallet authentication using MiniKit's hooks:

1. Import necessary hooks:
import { useAuthenticate, useFarcasterContext } from 'minikit';
import { useState } from 'react';

2. Create authentication handler in page.tsx:
export default function HomePage() {
  const { signIn } = useAuthenticate();
  const context = useFarcasterContext();
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  const handleSignIn = async () => {
    const result = await signIn({
      domain: process.env.NEXT_PUBLIC_APP_DOMAIN,
      siweUri: `${process.env.NEXT_PUBLIC_APP_URL}/login`
    });

    if (result) {
      setIsLoggedIn(true);
      console.log('Authentication successful');
    }
  };

  return (
    <div>
      {!isLoggedIn ? (
        <button onClick={handleSignIn}>
          Login with Farcaster
        </button>
      ) : (
        <div>
          <h1>Welcome, {context?.user?.username}!</h1>
        </div>
      )}
    </div>
  );
}
```

## Prompt 4: First Login Confetti
```
Add a celebratory confetti effect for new users:

1. Install react-confetti:
npm install react-confetti

2. Update page.tsx to include confetti:
import Confetti from 'react-confetti';

export default function HomePage() {
  // ... previous authentication code

  return (
    <div>
      {!isLoggedIn ? (
        <button onClick={handleSignIn}>
          Login with Farcaster
        </button>
      ) : (
        <div>
          {context?.user?.isNewUser && <Confetti />}
          <h1>Welcome, {context?.user?.username}!</h1>
        </div>
      )}
    </div>
  );
}
```

## Prompt 5: Manifest Configuration
```
Prepare manifest.json for Vercel deployment:

Create /public/manifest.json with:
{
  "name": "My Mini App",
  "description": "A MiniKit Mini App with Farcaster authentication",
  "icons": [
    {
      "src": "/icon.png",
      "sizes": "192x192",
      "type": "image/png"
    }
  ]
}

Ensure you have a 192x192 icon in /public/icon.png
```

## Prompt 6: Vercel Deployment
```
Deploy to Vercel:

1. Ensure you have Vercel CLI installed:
npm install -g vercel

2. Login to Vercel:
vercel login

3. Deploy the project:
vercel

4. Set environment variables in Vercel dashboard:
- NEXT_PUBLIC_APP_DOMAIN
- NEXT_PUBLIC_APP_URL
- FARCASTER_MNEMONIC (if required)

Verify deployment URL and test Farcaster login
```

## Final Verification Prompt
```
Conduct a comprehensive test of your MiniKit Mini App:

1. Verify login button appears
2. Click login and complete Farcaster authentication
3. Confirm username displays after login
4. Check if confetti appears for new users
5. Ensure smooth navigation and error handling
```

This promptorial provides a step-by-step guide to building a MiniKit Mini App with Farcaster authentication, deployed on Vercel, complete with a welcoming user experience.