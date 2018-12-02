> Demo for https://stackoverflow.com/q/53431754/6277151

This demo configures this Vue CLI project to enable Shadow CSS in Vue
web components with hot module reloading. The only change needed here
is to add [`<projectroot>/vue.config.js`](https://cli.vuejs.org/config/#vue-config-js)
with the following contents:

    function enableShadowCss(config) {
      const setShadowModeOption = (options) => {
        options.shadowMode = true;
        return options;
      };

      const cssProcessors = [
        'css',
        'stylus',
        'less',
        'sass',
        'scss',
        'postcss'
      ];
      const moduleTypes = [
        'normal',
        'normal-modules',
        'vue',
        'vue-modules',
      ];

      for (const p of cssProcessors) {
        for (const m of moduleTypes) {
          config.module
            .rule(p)
            .oneOf(m)
            .use('vue-style-loader')
            .loader('vue-style-loader')
            .tap(setShadowModeOption);
        }
      }

      config.module
        .rule('vue')
        .use('vue-loader')
        .loader('vue-loader')
        .tap(setShadowModeOption);
    }

    module.exports = {
      chainWebpack: config => {
        enableShadowCss(config);
      }
    }
