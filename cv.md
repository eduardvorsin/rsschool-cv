# Eduard Vorsin
## Contacts:
- **Location:** Kazakhstan, Karaganda
- **Phone:** +7(747)471-27-60
- **E-mail:** [eduardvorsin2019@gmail.com](mailto:eduardvorsin2019@gmail.com)
- **GitHub:** [eduardvorsin](https://github.com/eduardvorsin)
  
## Summary
As a frontend developer, I like to turn a finished design into a working application, paying attention to details and user experience. I like to explore new approaches and technologies that are used in production to solve various tasks in development

## Skills
- HTML
- CSS
- JavaScript
- React
- TypeScript
- Redux
- Tailwind
- Next JS
- i18next
- Git
- Figma

## **Code Example**
Example of a button component using React and Typescript:
```typescript
import { FocusEventHandler, MouseEventHandler, ReactNode } from 'react';
import Spinner from '@/components/Spinner/Spinner';
import Link from 'next/link';
import { GeneralProps } from '@/types/shared';

type ConditionalProps =
	{
		href: string,
		type?: never,
		isLoading?: never
	} | {
		href?: never,
		type?: HTMLButtonElement['type'],
		isLoading?: boolean,
	};

export type Props = {
	appearance?: 'primary' | 'secondary' | 'warning' | 'danger' | 'success' | 'discovery' | 'ghost',
	isDisabled?: boolean,
	onBlur?: FocusEventHandler<HTMLElement>,
	onClick?: MouseEventHandler<HTMLElement>,
	onFocus?: FocusEventHandler<HTMLElement>,
	size?: 'micro' | 'slim' | 'medium' | 'large',
	children: ReactNode,
	iconButton?: boolean,
} & ConditionalProps & GeneralProps;

const appearanceTypes = {
	primary: 'bg-blue-700 text-neutral-0 dark:text-dark-neutral-0 enabled:hover:bg-blue-800 enabled:active:bg-blue-900 dark:bg-blue-400 dark:enabled:hover:bg-blue-300 dark:enabled:active:bg-blue-200',
	secondary: 'bg-neutral-300 text-dark-neutral-0 enabled:hover:bg-neutral-400 enabled:active:bg-neutral-500 dark:enabled:hover:bg-neutral-200 dark:enabled:active:bg-neutral-100',
	success: 'bg-green-700 text-neutral-0 dark:text-dark-neutral-0 enabled:hover:bg-green-800 enabled:active:bg-green-900 dark:bg-green-400 dark:enabled:hover:bg-green-300 dark:enabled:active:bg-green-200',
	discovery: 'bg-purple-700 text-neutral-0 dark:text-dark-neutral-0 enabled:hover:bg-purple-800 enabled:active:bg-purple-900 dark:bg-purple-400 dark:enabled:hover:bg-purple-300 dark:enabled:active:bg-purple-200',
	danger: 'bg-red-700 text-neutral-0 dark:text-dark-neutral-0 enabled:hover:bg-red-800 enabled:active:bg-red-900 dark:bg-red-400 dark:enabled:hover:bg-red-300 dark:enabled:active:bg-red-200',
	warning: 'bg-yellow-500 text-neutral-1000 enabled:hover:bg-yellow-600 enabled:active:bg-yellow-700 dark:enabled:hover:bg-yellow-300 dark:enabled:active:bg-yellow-200',
	ghost: 'text-dark-neutral-0 enabled:hover:text-dark-neutral-400 enabled:active:text-dark-neutral-600 dark:text-neutral-200 dark:enabled:hover:text-neutral-400 dark:enabled:active:text-neutral-600',
} as const;

const iconButtonAppearances = {
	primary: 'text-blue-700 enabled:hover:text-blue-800 enabled:active:text-blue-900 dark:text-blue-400 dark:enabled:hover:text-blue-300 dark:enabled:active:text-blue-200',
	secondary: 'text-neutral-600 enabled:hover:text-neutral-700 enabled:active:text-neutral-800 dark:text-neutral-300 dark:enabled:hover:text-neutral-200 dark:enabled:active:text-neutral-100',
	success: 'text-green-700 enabled:hover:text-green-800 enabled:active:text-green-900 dark:text-green-400 dark:enabled:hover:text-green-300 dark:enabled:active:text-green-200',
	discovery: 'text-purple-700 enabled:hover:text-purple-800 enabled:active:text-purple-900 dark:text-purple-400 dark:enabled:hover:text-purple-300 dark:enabled:active:text-purple-200',
	danger: 'text-red-700 enabled:hover:text-red-800 enabled:active:text-red-900 dark:text-red-400 dark:enabled:hover:text-red-300 dark:enabled:active:text-red-200',
	warning: 'text-yellow-500 enabled:hover:text-yellow-600 enabled:active:text-yellow-700 dark:enabled:hover:text-yellow-300 dark:enabled:active:text-yellow-300',
	ghost: 'text-dark-neutral-0 enabled:hover:text-dark-neutral-400 enabled:active:text-dark-neutral-600 dark:text-neutral-0 dark:enabled:hover:text-neutral-400 dark:enabled:active:text-neutral-600',
} as const;

const sizeTypes = {
	micro: 'py-0.5 px-2',
	slim: 'py-1 px-3',
	medium: 'py-2 px-4',
	large: 'py-3 px-6',
} as const;

export default function Button({
	className,
	appearance = 'primary',
	isLoading,
	isDisabled,
	onBlur,
	onClick,
	onFocus,
	size = 'medium',
	children,
	href,
	iconButton,
	type,
	testId,
	...props
}: Props) {
	const currentFontSize = size === 'large' ? 'text-200' : 'text-100';
	const classes = [
		'items-center font-medium rounded-1 text-center cursor-pointer min-w[2.25rem] leading-2 inline-flex transition-colors duration-150',
		iconButton ? 'text-0' : currentFontSize,
		isDisabled ? 'opacity-disabled cursor-not-allowed' : '',
		iconButton ? iconButtonAppearances[appearance] : appearanceTypes[appearance],
		iconButton ? '' : `${sizeTypes[size]} relative`,
		isLoading ? 'pointer-events-none text-transparent dark:text-transparent select-none' : '',
		className,
	].join(' ');

	const Children =
		(<>
			{!iconButton && isLoading && (
				<Spinner
					className={`[&]:w-auto [&]:h-[80%] stroke-1 absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 ${appearance === 'secondary' ? 'text-dark-neutral-0' : 'text-neutral-0'}`}
					testId='spinner'
				/>
			)}

			<span
				className={'inline-flex items-center'}
			>
				{children}
			</span>
		</>);

	if (typeof href === 'string') {
		return (
			<Link
				className={classes}
				href={href}
				onClick={onClick}
				onBlur={onBlur}
				onFocus={onFocus}
				data-testid={testId}
				{...props}
			>
				{Children}
			</Link>
		);
	}

	return (
		<button
			className={classes}
			onClick={onClick}
			onBlur={onBlur}
			onFocus={onFocus}
			disabled={isDisabled}
			type={type}
			data-testid={testId}
			{...props}
		>
			{Children}
		</button>
	);
};
```

## Education
- **Bachelors**, Mechanics and Robotics at Karaganda Buketov University, 2020-2024
- **Masters**, Information systems and technologies, 2024-2026(in progress)

## Experience
- **Teacher of the React course** at [Almaty IT Step](https://almaty.itstep.org/), Sep 1-24 - present

## Languages
- **Russian** - native
- **English** - B2
