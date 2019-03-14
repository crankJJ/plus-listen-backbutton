<script>
			var plusReady = function(callback) {
				if (window.plus) {
					callback();
				} else {
					document.addEventListener('plusready', callback);
				}
			};
			plusReady(function() {
				var firstBack = 0;
				var handleBack = function() {
					var now = Date.now || function() {
						return new Date().getTime();
					};
					if (location.hash == '#/app/xindex') {
						if (!firstBack) {
							firstBack = now();
							plus.nativeUI.toast('再按一次退出应用');
							setTimeout(function() {
								firstBack = 0;
							}, 2000);
						} else if (now() - firstBack < 2000) {
							plus.runtime.quit();
						}
					} else {
						// console.log(location.hash);
						history.back();
					}
				};
				plus.key.addEventListener('backbutton', handleBack);
			});
		</script>