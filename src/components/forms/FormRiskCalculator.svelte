<script lang="ts">
	import z from 'zod';
	import clsx from 'clsx';

	const formData = {
		totalAccount: 15000,
		highPrice: 100,
		lowPrice: 80,
		riskInPercentage: 2,
	};

	const calculation = {
		totalRisk: {
			title: 'Total Risk',
			value: 0,
			additionalClasses: '',
		},

		entryAt: {
			title: 'Entry At',
			value: 0,
			additionalClasses: '',
		},

		stopLossAt: {
			title: 'Stop Loss',
			value: 0,
			additionalClasses: '',
		},

		exitAt: {
			title: 'Exit',
			value: 0,
			additionalClasses: '',
		},

		stopLossInMoney: {
			title: 'Stop Loss (in money)',
			value: 0,
			additionalClasses: '',
		},

		totalQuantity: {
			title: 'Total Quantity',
			value: 0,
			additionalClasses: '',
		},

		totalOrder: {
			title: 'Total Order Amount',
			value: 0,
			additionalClasses: '',
		},

		totalTradeInProfit: {
			title: 'Total Trade (in profit)',
			value: 0,
			additionalClasses: 'bg-green-100',
		},

		totalTradeInLoss: {
			title: 'Total Trade (in loss)',
			value: 0,
			additionalClasses: 'bg-red-100',
		},
	}

	const formValidationSchema = z.object({
		totalAccount: z.number().min(100),
		highPrice: z.number().min(0.2),
		lowPrice: z.number().min(0.1),
		riskInPercentage: z.number().min(0.5),
	});

	const calculate = async () => {
		try {
			const validatedData = await formValidationSchema.parseAsync(formData);

			const entryAtLeadingIncrement = 0.4;
			const entryAtLeadingMin = 0.75;
			let entryAtLeading = +((validatedData.highPrice / 100) * entryAtLeadingIncrement).toFixed(2);
			entryAtLeading = entryAtLeading > entryAtLeadingMin ? entryAtLeading : entryAtLeadingMin;
	
			calculation.totalRisk.value = Math.floor((validatedData.totalAccount / 100) * validatedData.riskInPercentage);
			calculation.entryAt.value = +(validatedData.highPrice + entryAtLeading).toFixed(2);
			calculation.stopLossAt.value = validatedData.lowPrice - Math.ceil(validatedData.lowPrice / 100);
			calculation.stopLossInMoney.value = +(calculation.entryAt.value - calculation.stopLossAt.value).toFixed(2);
			calculation.exitAt.value = calculation.entryAt.value + Math.floor(calculation.stopLossInMoney.value * 3);
			calculation.totalQuantity.value = Math.ceil(calculation.totalRisk.value / calculation.stopLossInMoney.value);
			calculation.totalOrder.value = Math.floor(calculation.entryAt.value * calculation.totalQuantity.value);
			calculation.totalTradeInProfit.value = Math.floor(calculation.exitAt.value * calculation.totalQuantity.value);
			calculation.totalTradeInLoss.value = Math.floor(calculation.stopLossAt.value * calculation.totalQuantity.value);
		} catch (err) {
			console.log(err);
		}
	}

	const onFormSubmit = () => {
		formData.totalAccount = +formData.totalAccount;
		formData.highPrice = +formData.highPrice;
		formData.lowPrice = +formData.lowPrice;
		formData.riskInPercentage = +formData.riskInPercentage;

		calculate();
	};
	
	calculate();
</script>

<section class="w-full sm:max-w-5xl mx-auto">
	<div class="section-header text-center mb-10">
		<h1 class="text-2xl md:text-4xl font-semibold text-gray-900">Stocks Risk & Quantity Calculator</h1>
	</div>
	<div class="section-body grid grid-cols-1 gap-4 md:grid-cols-2">
		<div class="bg-white rounded-lg shadow">
			<div class="p-6 space-y-4 md:space-y-6 sm:p-8">
				<h2 class="text-xl font-bold leading-tight text-center tracking-tight text-gray-900 md:text-2xl">Risk Calculator</h2>
				<form class="space-y-4 md:space-y-6" on:submit|preventDefault={ onFormSubmit }>
					<div class="form-group">
						<label for="txtTotalAccount" class="block mb-2 text-sm font-medium text-gray-900">Total Account</label>
						<input type="text" name="totalAccount" id="txtTotalAccount" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5" bind:value={ formData.totalAccount }/>
					</div>
					<div class="form-group">
						<label for="txtPreviousHighPrice" class="block mb-2 text-sm font-medium text-gray-900">Previous High Price</label>
						<input type="text" name="highPrice" id="txtPreviousHighPrice" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5" bind:value={ formData.highPrice }/>
					</div>
					<div class="form-group">
						<label for="txtPreviousLowPrice" class="block mb-2 text-sm font-medium text-gray-900">Previous Low Price</label>
						<input type="text" name="lowPrice" id="txtPreviousLowPrice" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5" bind:value={ formData.lowPrice }/>
					</div>
					<div class="form-group">
						<label for="txtRiskInPercentage" class="block mb-2 text-sm font-medium text-gray-900">Total Risk (in percentage)</label>
						<input type="text" name="riskInPercentage" id="txtRiskInPercentage" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5" bind:value={ formData.riskInPercentage }/>
					</div>
					<div class="form-actions">
						<button type="submit" class="w-full text-xl text-white bg-blue-600 hover:bg-blue-700 outline-none font-bold rounded-lg px-6 py-4 text-center">Calculate</button>
					</div>
				</form>
			</div>
		</div>
		<div class="bg-white rounded-lg shadow grid-cols-2">
			<div class="p-6 space-y-4 md:space-y-6 sm:p-8">
				<h2 class="text-xl font-bold leading-tight text-center tracking-tight text-gray-900 md:text-2xl">Calculations</h2>
				<div class="space-y-4 md:space-y-6">
					<ul class="border-2 rounded">
						{ #each Object.entries(calculation) as [key, item] }
							<li class={ clsx('px-4 py-2 border-b-2 last:border-0', item.additionalClasses) }>
								<span class="text-xl">{ item.title }:</span>
								<span class="text-xl font-bold">{ item.value }</span>
							</li>
						{ /each }
					</ul>
				</div>
			</div>
		</div>
	</div>
</section>