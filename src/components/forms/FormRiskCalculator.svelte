<section class="flex flex-col items-center justify-center">
	<div class="section-header text-center mb-6">
		<h1 class="text-5xl font-semibold text-gray-900">Stocks</h1>
	</div>
	<div class="section-body w-full sm:max-w-5xl grid grid-flow-row grid-cols-2 gap-4">
		<div class="bg-white rounded-lg shadow">
			<div class="p-6 space-y-4 md:space-y-6 sm:p-8">
				<h2 class="text-xl font-bold leading-tight text-center tracking-tight text-gray-900 md:text-2xl">Risk Calculator</h2>
				<form class="space-y-4 md:space-y-6" action="#">
					<div class="form-group">
						<label for="txtTotalAccount" class="block mb-2 text-sm font-medium text-gray-900">Total Account</label>
						<input type="text" name="totalAccount" id="txtTotalAccount" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5"/>
					</div>
					<div class="form-group">
						<label for="txtCurrentHighPrice" class="block mb-2 text-sm font-medium text-gray-900">Current High Price</label>
						<input type="text" name="currentHighPrice" id="txtCurrentHighPrice" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5"/>
					</div>
					<div class="form-group">
						<label for="txtCurrentLowPrice" class="block mb-2 text-sm font-medium text-gray-900">Current Low Price</label>
						<input type="text" name="currentLowPrice" id="txtCurrentLowPrice" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5"/>
					</div>
					<div class="form-group">
						<label for="txtRiskInPercentage" class="block mb-2 text-sm font-medium text-gray-900">Total Risk (in percentage)</label>
						<input type="text" name="riskInPercentage" id="txtRiskInPercentage" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5"/>
					</div>
					<div class="form-actions">
						<button type="submit" class="w-full text-white bg-blue-600 hover:bg-blue-700 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center">Calculate</button>
					</div>
				</form>
			</div>
		</div>
		<div class="bg-white rounded-lg shadow grid-cols-2">
			<div class="p-6 space-y-4 md:space-y-6 sm:p-8">
				<h2 class="text-xl font-bold leading-tight text-center tracking-tight text-gray-900 md:text-2xl">Results</h2>
			</div>
		</div>
	</div>
</section>