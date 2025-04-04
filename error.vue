<script setup lang="ts">
import WBtn from './components/shared/w-ui/WBtn';

defineProps<{
	error: {
		url: string;
		statusCode: 401 | 403 | 404 | 500;
		statusMessage: string;
		message: string;
		stack: string;
	};
}>();

const { t } = useI18n();

const errorDetails: Record<
	401 | 403 | 404 | 500,
	{
		type: string;
		title: string;
		description: string;
		photo: string;
	}
> = {
	401: {
		type: "401",
		title: "401.title",
		description: "401.description",
		photo: "/img/errors/401.svg",
	},
	403: {
		type: "403",
		title: "403.title",
		description: "403.description",
		photo: "/img/errors/403.svg",
	},
	404: {
		type: "404",
		title: "404.title",
		description: "404.description",
		photo: "/img/errors/404.svg",
	},
	500: {
		type: "500",
		title: "500.title",
		description: "500.description",
		photo: "/img/errors/500.svg",
	},
};

const handleError = () => clearError({ redirect: "/" });
</script>

<template>
	<div class="flex min-h-screen w-full items-center justify-center bg-white md:px-24 md:py-20 xl:px-40 xl:py-20">
		<Head>
			<Title>{{ error.statusCode }}</Title>
			<Meta name="description" :content="error.statusMessage" />
		</Head>
		<div class="flex h-full w-full flex-row flex-wrap items-center justify-center gap-8 rounded-lg px-10 py-4">
			<img :src="errorDetails[error.statusCode].photo" alt="Error" class="w-full max-w-md" />
			<div class="flex w-full max-w-md flex-col gap-4 text-center text-lg">
				<span class="block text-9xl font-bold">
					{{ errorDetails[error.statusCode].type }}
				</span>
				<span class="block">{{ t(`error.${errorDetails[error.statusCode].title}`) }}</span>
				<span class="block">
					{{ t(`error.${errorDetails[error.statusCode].description}`) }}
				</span>
				{{error}}
				<div class="mt-2 flex justify-center">
					<WBtn size="md" variant="primary" @click="handleError">
						{{ t("main_page") }}
					</WBtn>
				</div>
			</div>
		</div>
	</div>
</template>
